# Project-2d1
2d_top_down_action_roguelike, pc_single_play, Unity2D_C#


using UnityEngine;

[RequireComponent(typeof(Rigidbody2D))]
public class EnemyAI : MonoBehaviour
{
    [SerializeField] private float moveSpeed = 2f;
    [SerializeField] private float attackCooldown = 1f;
    [SerializeField] private int contactDamage = 1;

    private Rigidbody2D rb;
    private Transform player;
    private float nextAttackTime;

    private void Awake()
    {
        rb = GetComponent<Rigidbody2D>();
    }

    private void Start()
    {
        GameObject playerObject = GameObject.FindGameObjectWithTag("Player");

        if (playerObject != null)
        {
            player = playerObject.transform;
        }
        else
        {
            Debug.LogWarning("Player 태그가 지정된 오브젝트를 찾지 못했습니다.");
        }
    }

    private void FixedUpdate()
    {
        if (player == null)
            return;

        Vector2 direction =
            ((Vector2)player.position - rb.position).normalized;

        rb.MovePosition(rb.position + direction * moveSpeed * Time.fixedDeltaTime);
    }

    private void OnCollisionStay2D(Collision2D collision)
    {
        if (Time.time < nextAttackTime)
            return;

        PlayerHealth health = collision.gameObject.GetComponent<PlayerHealth>();

        if (health != null)
        {
            health.TakeDamage(contactDamage);
            nextAttackTime = Time.time + attackCooldown;
        }
    }
}
# Project-2d1
2d_top_down_action_roguelike, pc_single_play, Unity2D_C#

using UnityEngine;

public class PlayerAttack : MonoBehaviour
{
    [SerializeField] private Transform attackPoint;
    [SerializeField] private float attackRange = 1f;
    [SerializeField] private int attackDamage = 1;
    [SerializeField] private float attackCooldown = 0.4f;
    [SerializeField] private LayerMask enemyLayers;

    private float nextAttackTime;

    private void Update()
    {
        if(Input.GetKeyDown(KeyCode.Space) && Time.time >= nextAttackTime)
        {
            Attack();
            nextAttackTime = Time.time + attackCooldown;
        }
    }

    private void Attack()
    {
        Collider2D[] hitEnemies = Physics2D.OverlapCircleAll(
            attackPoint.position,
            attackRange,
            enemyLayers
        );

        foreach(Collider2D enemy in hitEnemies)
        {
            EnemyHealth health = enemy.GetComponent<EnemyHealth>();

            if(health != null)
            {
                health.TakeDamage(attackDamage);
            }
        }
        Debug.Log("공격!");
    }

    private void OnDrawGizmosSelected()
    {
        if(attackPoint != null)
        {
            Gizmos.color = Color.red;
            Gizmos.DrawWireSphere(attackPoint.position, attackRange);
        }
    }
}
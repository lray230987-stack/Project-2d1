# Project-2d1
2d_top_down_action_roguelike, pc_single_play, Unity2D_C#

using UnityEngine;

[RequireComponent(typeof(Rigidbody2D))]
public class PlayerController : MonoBehaviour
{
    [SerializeField] private float moveSpeed = 5f;

    private Rigidbody2D rb;
    private Vector2 moveInput;

    // 마지막으로 바라본 방향
    public Vector2 FacingDirection { get; private set; } = Vector2.down;

    private void Awake()
    {
        rb = GetComponent<Rigidbody2D>();
    }

    private void Update()
    {
        moveInput = Vector2.zero;

        if (Input.GetKey(KeyCode.UpArrow))
            moveInput.y += 1f;

        if (Input.GetKey(KeyCode.DownArrow))
            moveInput.y -= 1f;

        if (Input.GetKey(KeyCode.LeftArrow))
            moveInput.x -= 1f;

        if (Input.GetKey(KeyCode.RightArrow))
            moveInput.x += 1f;

        // 대각선 이동 속도가 더 빨라지지 않도록 보정
        moveInput = moveInput.normalized;

        // 이동 방향을 그대로 바라보는 방향으로 사용
        if(moveInput != Vector2.zero)
        {
            FacingDirection = moveInput;
        }
    }

    private void FixedUpdate()
    {
        rb.linearVelocity = moveInput * moveSpeed;
    }
}
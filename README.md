# Project-2d1
2d_top_down_action_roguelike, pc_single_play, Unity2D_C#


using UnityEngine;

public class PlayerHealth : MonoBehaviour
{
    [SerializeField] private int maxHealth = 5;

    private int currentHealth;
    private bool isDead;

    private void Awake()
    {
        currentHealth = maxHealth;
    }

    public void TakeDamage(int damage)
    {
        if (isDead)
            return;

        currentHealth -= damage;
        currentHealth = Mathf.Max(currentHealth, 0);

        Debug.Log("플레이어 체력: " + currentHealth + " / " + maxHealth);

        if (currentHealth <= 0)
        {
            Die();
        }
    }

    private void Die()
    {
        isDead = true;

        Debug.Log("게임 오버!");

        // 사망하면 이동과 공격을 중지
        PlayerController controller = GetComponent<PlayerController>();
        PlayerAttack attack = GetComponent<PlayerAttack>();

        if (controller != null)
            controller.enabled = false;

        if (attack != null)
            attack.enabled = false;
    }
}

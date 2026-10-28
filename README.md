# Project-2d1
2d_top_down_action_roguelike, pc_single_play, Unity2D_C#

using UnityEngine;

public class EnemyHealth : MonoBehaviour
{
    [SerializeField] private int maxHealth = 3;

    private int currentHealth;

    private void Awake()
    {
        currentHealth = maxHealth;
    }

    public void TakeDamage(int damage)
    {
        currentHealth -= damage;

        Debug.Log("적이 피해를 입었습니다! 남은 체력: " + currentHealth);

        if(currentHealth <= 0)
        {
            Destroy(gameObject);
        }
    }
}
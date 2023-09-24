# Penguin-Run

using UnityEngine;

public class PenguinController : MonoBehaviour
{
    public float moveSpeed = 5f;
    public float jumpForce = 10f;
    private bool isGrounded = true;
    private Rigidbody2D rb;

    void Start()
    {
        rb = GetComponent<Rigidbody2D>();
    }

    void Update()
    {
        // Check if the penguin is on the ground
        isGrounded = Physics2D.OverlapCircle(transform.position, 0.2f, LayerMask.GetMask("Ground"));

        // Horizontal movement
        float moveDirection = Input.GetAxis("Horizontal");
        Vector2 move = new Vector2(moveDirection * moveSpeed, rb.velocity.y);
        rb.velocity = move;

        // Jump
        if (isGrounded && Input.GetKeyDown(KeyCode.W))
        {
            rb.AddForce(Vector2.up * jumpForce, ForceMode2D.Impulse);
        }

        // Duck (move down)
        if (Input.GetKey(KeyCode.S))
        {
            // You can implement ducking behavior here, e.g., crouching animation or changing collider size.
        }
    }
}

using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class CameraFollowObject : MonoBehaviour
{
    [Header("References")]
    [SerializeField] private Transform playerTransform;

    [Header("Flip Rotation Stats")]
    [SerializeField] private float flipVRotationTime = 0.5f;

    private Coroutine turnCoroutine;

    private Player player;

    private bool isFacingRight;

    private void Awake()
    {
        player = playerTransform.gameObject.GetComponent<Player>();
        isFacingRight = player.isFacingRight;
    }

    private void Update()
    {
        // Make the cameraFollowObject follow the player's position
        transform.position = playerTransform.position;
    }

    public void CallTurn()
    {
        LeanTween.rotateY(gameObject, DetermineEndRotation(), flipVRotationTime).setEaseInOutSine();
    }

    private IEnumerator FlipLerp()
    {
        float startRotation = transform.localEulerAngles.y;
        float endRotationAmount = DetermineEndRotation();
        float yRotation = 0f;

        float elapsedTime = 0f;
        while (elapsedTime < flipVRotationTime)
        {
            elapsedTime += Time.deltaTime;

            // Lerp the y rotation
            yRotation = Mathf.Lerp(startRotation, endRotationAmount, (elapsedTime / flipVRotationTime));
            transform.rotation = Quaternion.Euler(0f, yRotation, 0f);

            yield return null;
        }
    }

    private float DetermineEndRotation()
    {
        isFacingRight = !isFacingRight;

        if (isFacingRight)
        {
            return 0f;
        }
        else
        {
            return 180f;
        }
    }
}

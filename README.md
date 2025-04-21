# LampTales Payment Status Page

## Description

This HTML page serves as a status indicator and redirect mechanism after a user completes (or cancels) a payment process initiated from the LampTales application. It informs the user about the payment outcome (success, cancellation, or processing) and automatically redirects them back to the LampTales mobile app using a custom deep link (`lamptales://`). A manual redirect button is also provided as a fallback.

## Features

*   **Payment Status Display:** Clearly shows whether the payment was successful, cancelled, or is still processing based on URL parameters.
*   **Automatic Redirect:** Attempts to automatically redirect the user back to the LampTales app after a short delay using a deep link.
*   **Manual Redirect Button:** Offers a button for users to manually trigger the redirect if the automatic process fails or is blocked.
*   **Deep Linking:** Constructs a `lamptales://` deep link, passing relevant `session_id` and `payment_id` back to the app.
*   **Responsive Design:** Adapts to different screen sizes.
*   **Theming:** Supports both light and dark color schemes based on user's system preference (`prefers-color-scheme`).
*   **Visual Feedback:** Includes a loading spinner while waiting for the redirect.
*   **Glassmorphism UI:** Uses modern CSS techniques for a blurred background effect on the main container.

## How it Works

1.  **URL Parameters:** The page expects URL query parameters to determine the status and necessary identifiers:
    *   `status`: Should be 'success' or 'cancel'. If absent or different, it defaults to a "Processing" state.
    *   `session_id` (Optional): The session identifier from the payment process.
    *   `payment_id` (Optional): The specific payment transaction identifier.
2.  **Status Update:** JavaScript reads these parameters and updates the displayed message and its styling (e.g., green text for success, red for cancel).
3.  **Deep Link Construction:** It constructs a deep link in the format `lamptales://payment/[status]?session_id=[session_id]&payment_id=[payment_id]`. The status path will be `success` or `cancel`. Parameters are appended only if present in the URL.
4.  **Redirection:**
    *   The script sets the `href` of the "Return to App" button to the constructed deep link.
    *   It initiates an automatic redirect to the deep link using `window.location.href` after a 1.5-second delay (`setTimeout`).

## Usage / Integration

This page is designed to be used as the `success_url` and `cancel_url` (or equivalent) in a payment gateway integration (like Stripe Checkout, PayPal, etc.).

*   When setting up the payment session, provide this page's URL as the redirect target.
*   Ensure the payment gateway appends the status (`success` or `cancel`) and any required identifiers (`session_id`, `payment_id`) as query parameters to the redirect URL.

**Example Redirect URLs:**

*   `https://yourdomain.com/payment-status.html?status=success&session_id=cs_123&payment_id=pi_456`
*   `https://yourdomain.com/payment-status.html?status=cancel&session_id=cs_123`

## Customization

*   **Deep Link Scheme:** If your app uses a different deep link scheme than `lamptales://`, update the `deepLink` variable construction in the `<script>` section accordingly.
*   **Styling:** Modify the CSS within the `<style>` tags or link an external stylesheet to change the appearance. Color variables for themes are defined in the `:root` selector.
*   **Redirect Delay:** Adjust the `setTimeout` duration (currently 1500ms) if needed.

## Technologies Used

*   HTML
*   CSS (including CSS Variables and Media Queries)
*   JavaScript (Vanilla)

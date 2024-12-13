---
title: Redirection
lang: en-US
---

# Redirection

After submitting a form, the user will be redirected to a generic [feedback page](/customization/feedback-page) hosted by Formspark.

This default behavior can be overridden in multiple ways.

## Specifying a custom redirect URL

1. Add an input of type `hidden`.
2. Set the input's name to `_redirect`.
3. Set the value to the URL you want to redirect users to.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Subscribe to Our Newsletter</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: linear-gradient(to bottom right, #6a11cb, #2575fc);
      color: white;
      text-align: center;
      padding: 2rem;
    }
    form {
      background: rgba(255, 255, 255, 0.2);
      border-radius: 10px;
      padding: 2rem;
      display: inline-block;
      box-shadow: 0 8px 15px rgba(0, 0, 0, 0.2);
    }
    input[type="email"] {
      width: 80%;
      padding: 0.5rem;
      margin-bottom: 1rem;
      border: none;
      border-radius: 5px;
    }
    button {
      background-color: #ff6f61;
      color: white;
      border: none;
      padding: 0.8rem 2rem;
      border-radius: 5px;
      cursor: pointer;
      font-size: 1rem;
    }
    button:hover {
      background-color: #ff4c3b;
    }
    h1 {
      margin-bottom: 1rem;
    }
    p {
      font-size: 1rem;
      opacity: 0.8;
    }
  </style>
</head>
<body>

  <h1>Subscribe to Our Newsletter!</h1>
  <p>Be the first to know about our updates and exclusive offers.</p>

  <form action="https://submit-form.com/your-form-id">
    <!-- Redirect hidden input -->
    <input type="hidden" name="_redirect" value="https://your-website.com/thank-you" />
    <!-- Email input -->
    <input type="email" name="email" placeholder="Enter your email" required />
    <!-- Submit button -->
    <button type="submit">Subscribe Now</button>
  </form>

</body>
</html>

```

By default, Formspark appends the submission's entries to the custom redirect URL (to its search string).
This enables you to personalize your page with user-submitted data.

The above form's submissions would redirect to `https://your-website.com/thanks?email=example%40email.com`.

You can toggle off this behavior by adding a hidden input with the name `_append` and the value `false`.

```html
<input type="hidden" name="_append" value="false" />
```

## Specifying a custom error redirect URL

Note: If you don't specify a custom error redirect URL then the configuration from `_redirect` (if present) will
automatically be inherited.

1. Add an input of type `hidden`.
2. Set the input's name to `_error`.
3. Set the value to the URL you want to redirect users to.

```html
<form action="https://submit-form.com/your-form-id">
  <input type="hidden" name="_error" value="https://your-website.com/error" />
  <input type="email" name="email" />
  <button type="submit">Subscribe</button>
</form>
```

## Preventing the redirect

### Staying on the same page (without leaving it)

This is only possible with JavaScript/AJAX.

Formspark has excellent AJAX support, [learn more about it here](/examples/ajax.html).

### Returning to the same page (after leaving it)

```html
<!--
1. If your form is hosted at "https:/my-website.com/newsletter.html"
-->
<form action="https://submit-form.com/your-form-id">
  <!-- 2. Then you would set the "_redirect" to "https:/my-website.com/newsletter.html" -->
  <input
    type="hidden"
    name="_redirect"
    value="https:/my-website.com/newsletter.html"
  />
  <input type="email" name="email" />
  <button type="submit">Subscribe</button>
</form>
```

This method is based on illusion. Technically, you are not preventing the redirection.

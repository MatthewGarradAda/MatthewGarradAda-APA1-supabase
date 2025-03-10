# Supabase Backend

Edge Functions and Database triggers for order processing and email notifications.

## Features
- Automated email confirmations on new orders
- PostgreSQL database triggers
- Secure credentials with git ingored file

## Quickstart

1. Create and export credentials in `config.ts`:
```typescript
// config.ts
export const EMAIL_USER = 'your-email@domain.com'
export const EMAIL_APP_PASSWORD = 'your-app-password'
```

2. Deploy to Supabase:
```bash
supabase link
supabase db push
supabase deploy email_confirmation
```

## Local Development

Start local Supabase instance:
```bash
supabase link
supabase start
supabase functions serve
```

## Edge Functions

`email_confirmation` - Sends order confirmation emails using:
- Gmail API for email delivery
- Order details from database trigger
- Secure credential management

## Testing
Test email function locally:
```bash
supabase functions serve email_confirmation
curl -i --location --request POST 'http://localhost:54321/functions/v1/email_confirmation' \
  --header 'Authorization: Bearer YOUR_ANON_KEY' \
  --data '{
    "order": {
      "id": 123,
      "email": "customer@example.com",
      "address1": "123 Test Street",
      "address2": "Apt 4B",
      "city": "Test City", 
      "postcode": "TE1 1ST",
      "products": [
        {
          "id": 1,
          "name": "Test Product",
          "price": "99.99",
          "quantity": 2,
          "sku": "TEST123"
        }
      ],
      "total": "199.98",
      "created_at": "2024-01-20T12:00:00Z"
    }
  }'
```
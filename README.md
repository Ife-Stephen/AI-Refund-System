# AI Refund Support System — starter MVP

## Run with Docker Desktop

1. Ensure Docker Desktop is running.
2. From this project directory, create `.env` from `.env.example` if you do not already have `.env`.
3. Run:

   ```powershell
   docker compose up --build
   ```

4. Open:
   - Frontend: http://localhost:8080
   - API docs: http://localhost:8000/docs
   - Health: http://localhost:8000/health

Stop with `Ctrl+C`, then `docker compose down`. Database data is kept in the named volume. To delete the database volume as well, use `docker compose down -v` (destructive).

## Policy

Edit `policy/refund_policy.json`. The backend reads it when evaluating each new request. The current rules use a 30-day window, flag requests over $500 for review, reject final-sale items, and send damaged/wrong/not-received requests to review.

## AI

If `OPENAI_API_KEY` is empty, explanations use a deterministic fallback. If configured, the AI rewrites the policy explanation in plain language; it must not change the eligibility decision.

## Important limitations

This is a local-development MVP, not production-ready. Before using real customer information or exposing it publicly, add authentication and role-based authorization, protect customer lookup endpoints, add audit logging and rate limiting, validate order ownership and actual paid amounts against an order system, use migrations, and implement payment-provider integration with idempotency. The review endpoint is intentionally unauthenticated only for local testing. Do not treat eligibility as approval or payment.

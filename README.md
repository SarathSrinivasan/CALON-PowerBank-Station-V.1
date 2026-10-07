# CALON PowerBank Station — MQTT Frontend Test Build

Frontend-only GitHub Pages test build for CALON PowerBank Station.

## Final rental protocol
1. Station QR opens `rent.html`.
2. WEB publishes `RENT_REQUESTED` → `POWERBANK/001/RENT_REQUEST`.
3. WEB publishes selected rental plan → `POWERBANK/001/RENT_PLAN`.
4. STM32 publishes `AVAILABILITY` → `POWERBANK/001/AVAILABILITY`.
5. WEB moves to the separate selection page.
6. WEB publishes `POWERBANK_SELECTED` → `POWERBANK/001/POWERBANK_SELECT`.
7. WEB publishes `PAYMENT_SUCCESS` → `POWERBANK/001/PAYMENT`.
8. STM32 physically opens the selected slot.
9. STM32 publishes `SLOT_OPENED` → `POWERBANK/001/SLOT_STATUS`.
10. WEB shows Thank You / Welcome.

## Final return protocol
1. Customer scans the PowerBank QR or enters its ID.
2. WEB publishes `RETURN_REQUESTED` → `POWERBANK/001/RETURN_REQUEST`.
3. STM32 validates/completes the return.
4. STM32 publishes `RETURN_ACCEPTED` → `POWERBANK/001/RETURN_STATUS`.
5. WEB shows Thank You / Welcome.

## MQTT
Broker: `wss://broker.emqx.io:8084/mqtt`

This is a public development broker. Do not use it for production customer data.

## GitHub Pages
Recommended:
- Repository visibility: Public for the simplest GitHub Pages test.
- Pages source: Deploy from `main` branch, root `/`.
- Open the generated Pages URL over HTTPS.
- Station QR should point directly to `.../rent.html`.

## Test Console
`test-console.html` can simulate STM32 `AVAILABILITY`, `SLOT_OPENED`, and `RETURN_ACCEPTED` messages.

Do not use the test console as the production STM32 implementation.

## Important
The website never creates `SLOT_OPENED` as a hardware truth. Production STM32 must publish it only after the slot-open sensor confirms the physical slot opened.

---
name: deadline-delivery-check
description: >-
  Use whenever a request has a deadline ("by Friday", "before 5pm tomorrow") to
  keep only options that arrive in time.
---
Inputs: item and recommended size variant, deadline, ZIP, stored memberships.

1. Browser required. Set the ZIP and nearest pickup store on the site first.
2. Select the recommended size variant, then read the delivery promise and pickup stock. If the size changes later, re-check or mark "guess (seen for size X)".
3. A promise without a time doesn't meet a time-of-day deadline: list it under "Might not make it", labeled "time window not shown".
4. Compare pickup and shipping; keep the one that beats the deadline.
5. Label each option Arrives: seen or guess. Say "logged out view" when signed out.
6. Retry once on a block or 503, then skip and name the store. Cap at 3 stores or about 5 minutes.
7. If nothing makes it, say so first, then the closest seen option and a store to call.
Output: per option: date or window, pickup or ship, seen or guess, and item + shipping total with "tax not shown" unless tax is shown.

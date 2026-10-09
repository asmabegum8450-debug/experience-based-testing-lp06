# Learning Practice 6: Experience-Based Testing

## Application
North Vacation Booking

## Feature Tested
Add Booking and viewing reservations

## Step 1: Error Guessing

Three possible problems I predicted:

1. The booking form might allow invalid guest counts.
2. The application might allow bookings for dates in the past.
3. The Rental dropdown might fail to load available properties.

## Step 2: Exploratory Testing

### Testing Charter
Investigate whether users can create valid bookings, whether invalid information is rejected, and whether reservations remain available after navigation or refresh.

### Exploratory Testing Notes

| What I Tried | What Happened | What I Decided to Try Next |
|---|---|---|
| Opened Add Booking directly | Rental dropdown was empty | Check whether backend rentals were available |
| Opened backend rentals endpoint | Backend returned 10 properties | Visit Home before opening Add Booking |
| Visited Home, then Add Booking | Rental dropdown displayed properties | Test guest validation |
| Entered 0 guests | Browser prevented submission | Try a valid booking |
| Created a booking with valid information | Booking appeared in the Bookings page | Test invalid dates |
| Submitted a past booking date | Application accepted a booking dated November 10, 2025 | Check booking persistence |
| Refreshed the Bookings page | Previously displayed bookings disappeared | Investigate booking storage in a future session |

### Additional Testing Ideas
- Test duplicate reservations.
- Test unusually large guest counts.
- Investigate whether bookings are stored only in memory.

## Step 3: Checklist-Based Testing

| Check | Result | Notes |
|---|---|---|
| Create a valid booking | Passed | Booking appeared in the list |
| Reject zero guests | Passed | Browser blocked submission |
| Require a booking date | Passed | Browser prevented empty-date submission |
| Display rentals when opening Add Booking directly | Failed | Dropdown was empty until visiting Home |
| Reject booking dates in the past | Failed | November 10, 2025 was accepted |
| Preserve bookings after browser refresh | Failed | Bookings disappeared |

## Step 4: Acceptance Testing

| Given, When, Then | Result | Notes |
|---|---|---|
| Given I have selected a rental, when I enter a valid date and 2 guests and confirm, then my booking should appear in the Bookings list. | Passed | Valid reservation appeared |
| Given I am booking a stay, when I enter 0 guests, then the form should prevent submission. | Passed | Browser blocked submission |
| Given I open Add Booking directly, when the page loads, then I should be able to select an available rental. | Failed | Dropdown was empty |
| Given I select a date in the past, when I submit the booking, then the application should reject the date. | Failed | Past-date booking was accepted |
| Given I have created a reservation, when I refresh the Bookings page, then my reservation should remain visible. | Failed | Reservations disappeared after refresh |

## Conclusion

Experience-based testing helped me discover problems that might not be covered by basic test cases. The application correctly prevented zero guests and allowed valid bookings, but I identified issues with rental loading, past-date validation, and booking persistence.

The most important improvements would be loading rental data independently of navigation history, preventing past-date reservations, and preserving bookings after refresh.

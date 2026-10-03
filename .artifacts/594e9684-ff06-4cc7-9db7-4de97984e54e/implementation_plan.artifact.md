# Implement Friends Screen

This plan implements the detailed "Friends" screen in `friends_screen.dart` using the logic and UI provided. It handles loading friends, identifying those with an active GAP, and displaying them in organized sections ("With GAP now" and "In class").

## User Review Required

> [!WARNING]
> The provided `_buildInClassRow` uses `Expanded` for each friend in a `Row`. If you have more than 3 or 4 friends in class, this will likely cause a layout overflow or crash. I recommend using a `Wrap` or a horizontal scrollable list instead. I will use a `Wrap` to ensure it stays safe while keeping a similar look.

> [!NOTE]
> I will adjust the header padding to `EdgeInsets.fromLTRB(20, 14, 20, 14)` to match the "Schedule" and "Match" screens for visual consistency.

## Proposed Changes

### UI Components

#### [MODIFY] [friends_screen.dart](file:///D:/MOVILES/front/lib/screens/friends/friends_screen.dart)

- Replace the placeholder `StatelessWidget` with the full `StatefulWidget` implementation.
- Integrate `FriendshipService` and `GapService` to load data.
- Implement the "Free Now" cards with GAP window labels and a "MATCH" button.
- Implement the "In Class" section using a `Wrap` for safety.
- Use `withValues(alpha: ...)` for color consistency.
- Add pull-to-refresh functionality.

## Verification Plan

### Manual Verification
1. Navigate to the "Friends" tab.
2. Verify that the loading indicator appears.
3. Check that friends with active gaps are shown at the top with their specific gap times.
4. Verify that friends currently in class are shown in the secondary section.
5. Tap "Try again" if an error occurs.
6. Verify the "MATCH" button navigates to the pending match screen.

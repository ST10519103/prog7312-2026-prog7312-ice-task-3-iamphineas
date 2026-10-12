# PROG7312 ICE Task 3 – Album Collection & Debugging

## Student Information

**Student Number:** ST10519103  
**Module:** PROG7312 – Programming 3  
**Task:** ICE Task 3 – Album Collection & Debugging  
**Application:** Album Collection  
**Repository:** `ST10519103/prog7312-2026-prog7312-ice-task-3-iamphineas`

---

# 1. Introduction

This project is a React Native and TypeScript Album Collection application developed for PROG7312 ICE Task 3.

The purpose of this task was to investigate an existing React Native application containing intentional errors, identify the causes of those errors, correct the implementation, and test the application to confirm that it behaves as intended.

The application allows a user to enter information about an album, validate the information, add albums to a favourites collection, display the collection using a `FlatList`, and remove albums from the collection.

The task was approached as a debugging and code-understanding exercise rather than developing a new application from scratch.

---

# 2. Purpose of the Application

The Album Collection application allows the user to maintain a simple collection of favourite albums.

The application allows the user to:

- Enter an album title
- Enter an artist name
- Enter an album release year
- Select an album genre
- Enter a rating from 1 to 5
- Validate the information entered
- Add albums to the favourites collection
- Display multiple albums
- Delete individual albums
- Continue using the application after adding and deleting albums

The application uses React state to maintain the collection while the application is running.

---

# 3. Technologies Used

The application was developed using the following technologies:

- React Native
- Expo
- TypeScript
- React Native `FlatList`
- React Native `TextInput`
- React Native `TouchableOpacity`
- React Native `Alert`
- `@react-native-picker/picker`
- BlueStacks 5
- Expo Go
- Visual Studio Code

---

# 4. Development Environment

The application was developed and tested inside the institutional virtual machine environment as required by the task.

The application was tested using:

- **Development Environment:** Institutional VM
- **Code Editor:** Visual Studio Code
- **Framework:** React Native
- **Platform:** Expo
- **Language:** TypeScript
- **Android Emulator:** BlueStacks 5
- **Testing Application:** Expo Go

The application was launched through the Expo development server and tested on the Android environment provided by BlueStacks 5.

---

# 5. Application Structure

The application code for the Album Collection functionality is contained in `App.tsx`, as required by the task.

The main elements of the application include:

- `Album` type definition
- Album form state
- Album collection state
- Form validation
- Album creation
- Album deletion
- Genre selection
- `FlatList` collection display
- User feedback using alerts
- Styling using React Native `StyleSheet`

The application maintains album records in an array using React state.

---

# 6. Error Investigation

The supplied application contained multiple intentional problems.

The application was first examined and run before the corrections were made. The problems were then investigated by examining the code and interacting with the application.

The errors were not treated as a single compiler problem. Both code-level problems and runtime behaviour were investigated.

---

# 7. Error Log

| # | Location | Problem | Error Type | Correction |
|---|---|---|---|---|
| 1 | `Album` type | `year` and `rating` were declared as strings even though numeric values were assigned when an album object was created. | TypeScript / Type mismatch | Changed `year` and `rating` to `number` so the type matches the values stored in the album object. |
| 2 | Album title validation | The validation used `&&` when checking whether the title was below the minimum length and above the maximum length. Both conditions could not be true at the same time. | Logic error | Changed the condition to use `||` so that either an undersized or oversized title is rejected. |
| 3 | Artist validation | The artist validation contained the same incorrect `&&` logic as the album title validation. | Logic error | Changed the condition to use `||` so that invalid artist lengths are correctly rejected. |
| 4 | Rating validation | The supplied validation checked whether the rating was below 1 but did not reject ratings above the maximum value of 5. | Validation / Logic error | Added a maximum rating check so only ratings from 1 to 5 are accepted. |
| 5 | Genre Picker | The Picker used `title` as its `selectedValue` even though the Picker represents the selected genre. | State / UI error | Changed the Picker's `selectedValue` to use the `genre` state. |
| 6 | Genre Picker items | Each Picker item used the current `genre` as its value instead of the genre represented by the item in the `genres` array. | Logic error | Changed the Picker item value to `item`, allowing each genre option to correctly update the selected genre. |
| 7 | `handleSave` | The supplied code used `setAlbums([temporaryAlbum])`, which replaced the entire collection every time a new album was added. | State management error | Changed the state update so the new album is appended to the existing collection. |
| 8 | `handleDelete` | The supplied filter used `album.id === id`, which kept the selected album and removed the other albums. | Logic error | Changed the filter to `album.id !== id`, removing only the selected album. |
| 9 | `FlatList` key | The supplied `FlatList` used the album title as the key even though each album already had a unique ID. | List handling / Code quality | Changed the key extractor to use the unique album ID. |
| 10 | Collection layout | The album collection was initially difficult to reach on the mobile screen because the form occupied most of the available space. | UI / Usability issue | Adjusted the layout so the `FlatList` receives the remaining screen space and can scroll correctly. |

---

# 8. Dependency and Environment Issue

During the initial setup, the supplied application used the following Picker import:

`@expo/ui/community/picker`

The project was initially unable to resolve this module in the Expo environment being used.

The `@expo/ui` dependency was investigated and installed, but the supplied compatibility import continued to produce a module resolution error.

To allow the supplied application to run correctly in the Expo Go environment, the Picker was changed to the Expo-compatible React Native Picker package:

`@react-native-picker/picker`

This was treated as an environment and dependency compatibility issue rather than one of the application's intentional logic errors.

The rest of the application concept and required Album Collection functionality remained unchanged.

---

# 9. Form Validation

The corrected application validates the information before an album is added.

The following validation checks were implemented:

- Album title must be provided.
- Album title must contain between 2 and 50 characters.
- Artist name must be provided.
- Artist name must contain between 2 and 50 characters.
- Album year must be provided.
- Album year must be a whole number.
- Album year must not be earlier than 1900.
- Album year must not be later than the current year.
- A genre must be selected.
- A rating must be provided.
- Rating must be a whole number.
- Rating must be between 1 and 5.

Invalid information is rejected and an appropriate validation message is displayed to the user.

---

# 10. Adding Albums

When valid album information is submitted, an `Album` object is created.

Each album contains:

- Unique ID
- Album title
- Artist
- Release year
- Genre
- Rating

The album is then added to the existing collection using React state.

The corrected implementation ensures that adding a new album does not remove albums that were previously added.

For example, after adding three different albums, all three remain available in the collection.

---

# 11. Displaying Albums

The favourites collection is displayed using React Native's `FlatList`.

Each album displays:

- Album title
- Artist
- Year
- Genre
- Rating

The `FlatList` updates when albums are added or removed.

The list also provides an empty-state message when no albums have been added.

---

# 12. Deleting Albums

Each album contains a Delete button.

When the Delete button is selected, the application asks the user to confirm the deletion.

After confirmation:

- The selected album is removed.
- Other albums remain in the collection.
- The collection count updates.
- The application remains usable.

This behaviour was tested with multiple albums in the collection.

---

# 13. User Feedback

The application provides feedback during important user interactions.

Validation errors are displayed using alerts when invalid information is entered.

A success message is displayed when an album has been successfully added.

A confirmation message is displayed before an album is deleted.

An empty-state message is displayed when the favourites collection contains no albums.

These features help the user understand what is happening during each action.

---

# 14. Testing

Testing was performed using the BlueStacks 5 Android emulator with Expo Go.

The following test scenarios were completed.

## Test 1 – Initial Application

**Action:**

Launch the application through Expo Go.

**Expected Result:**

The Album Collection interface should load without unexpected application errors.

**Result:**

PASS

The application launched successfully and displayed the Album Collection interface.
<img width="547" height="932" alt="image" src="https://github.com/user-attachments/assets/f407608d-ee7e-4dec-aa7e-6844d34d4706" />

---

## Test 2 – Empty Form Validation

**Action:**

Press `Add to Favourites` without entering album information.

**Expected Result:**

A validation message should appear and no album should be added.

**Result:**

PASS

The application displayed a validation error requesting an album title.
<img width="547" height="933" alt="image" src="https://github.com/user-attachments/assets/bd2479f7-630d-4c03-8e47-7d7047bd0dff" />

---

## Test 3 – Valid Album

**Action:**

Enter valid information for an album and submit the form.

**Expected Result:**

The album should be added to the favourites collection and displayed correctly.

**Result:**

PASS

The album was successfully added and displayed in the collection.
<img width="550" height="935" alt="image" src="https://github.com/user-attachments/assets/de04e11e-4e4a-462f-a3da-b6a502fe6a06" />

---

## Test 4 – Multiple Albums

**Action:**

Add multiple different albums.

**Expected Result:**

All albums should remain in the collection.

**Result:**

PASS

The collection count increased and previously added albums remained available.
<img width="538" height="943" alt="image" src="https://github.com/user-attachments/assets/8dd1ba8f-1b71-4f76-8806-9bc6620d5da0" />
<img width="537" height="941" alt="image" src="https://github.com/user-attachments/assets/92fe7ddf-73b9-46ab-a144-75cb7b3532c2" />

---

## Test 5 – Invalid Rating

**Action:**

Enter a rating greater than 5.

**Expected Result:**

The application should reject the rating.

**Result:**

PASS

The application rejected the invalid rating and displayed the appropriate validation message.
<img width="550" height="937" alt="image" src="https://github.com/user-attachments/assets/4f0d3175-cba5-4059-a4b6-200cd930a8b5" />

---

## Test 6 – Genre Selection

**Action:**

Open the genre Picker and select different genres.

**Expected Result:**

The selected genre should update correctly.

**Result:**

PASS

The Picker correctly displayed and stored the selected genre.
<img width="556" height="937" alt="image" src="https://github.com/user-attachments/assets/f0327749-0cbf-4ce1-a55a-0bb8aa44adf9" />

---

## Test 7 – Delete Album

**Action:**

Add multiple albums and delete one of them.

**Expected Result:**

Only the selected album should be removed while the other albums remain.

**Result:**

PASS

The selected album was removed and the remaining album records stayed in the collection.
<img width="542" height="817" alt="image" src="https://github.com/user-attachments/assets/cbf92df4-e25f-4513-85e4-37843d2ad26e" />

---

## Test 8 – Continued Use After Deletion

**Action:**

Continue interacting with the application after adding and deleting albums.

**Expected Result:**

The application should remain stable and continue accepting new information.

**Result:**

PASS

The application continued to operate correctly after album deletion.
<img width="541" height="942" alt="image" src="https://github.com/user-attachments/assets/148ec71a-7ad1-42db-b6ce-7ccae0718de4" />

---

# 15. Testing Summary

| Test | Description | Result |
|---|---|---|
| 1 | Initial application launch | PASS |
| 2 | Empty form validation | PASS |
| 3 | Valid album creation | PASS |
| 4 | Multiple album creation | PASS |
| 5 | Invalid rating validation | PASS |
| 6 | Genre selection | PASS |
| 7 | Album deletion | PASS |
| 8 | Continued use after deletion | PASS |

All required functional tests were completed successfully.

---

# 16. Completed Application Screenshot

The following screenshot shows the completed Album Collection application running in the BlueStacks 5 emulator using Expo Go.


<img width="553" height="936" alt="image" src="https://github.com/user-attachments/assets/c98689ec-f054-4fd9-80e4-a21f79e723eb" />

<img width="543" height="932" alt="image" src="https://github.com/user-attachments/assets/43baec6c-6b6b-40be-b6e4-5ec5bfd18266" />


---

# 17. Challenges Encountered

Several challenges were encountered during the debugging process.

### TypeScript Type Mismatch

The `Album` type initially defined `year` and `rating` as strings while numeric values were assigned to those properties. This required the type definition and stored values to be aligned.

### Incorrect Validation Logic

The title and artist length validation used logical AND conditions where OR conditions were required. Understanding the logical behaviour of these conditions was necessary to ensure invalid input was correctly rejected.

### State Management

The original album creation logic replaced the existing array whenever a new album was added. This demonstrated the importance of preserving existing state when adding new records.

### Delete Logic

The supplied delete filter retained the selected album instead of removing it. Testing with multiple albums made this problem clear.

### Picker Configuration

The genre Picker initially used the wrong state value and assigned the wrong value to each Picker option. Correcting these values allowed the selected genre to be stored correctly.

### Mobile Layout

The collection initially required additional layout adjustments because the form occupied most of the available mobile screen. The `FlatList` was adjusted so that the collection could be accessed and scrolled correctly.

---

# 18. Lessons Learned

This task provided practical experience in debugging an existing React Native and TypeScript application rather than simply writing an application from scratch.

The main lessons learned were:

- A compiler error may not be the only problem in an application.
- Runtime behaviour must be tested in addition to checking the code.
- Logical operators can significantly affect validation behaviour.
- React state must be updated carefully when working with arrays.
- Array filtering must be checked carefully when removing records.
- TypeScript types should accurately represent the values stored in objects.
- List components require appropriate keys for reliable rendering.
- User input should be validated before it is stored.
- Mobile layouts need to be tested on an actual emulator.
- Testing multiple records can reveal problems that are not visible when testing a single record.
- Existing code should be understood before making corrections.

---

# 19. Code Quality

The corrected application was kept within the supplied `App.tsx` structure.

The code uses:

- Meaningful variable names
- Meaningful function names
- TypeScript type definitions
- React state management
- Reusable validation logic
- Appropriate comments
- Consistent formatting
- `FlatList` for collection rendering
- Unique album IDs
- User feedback through alerts

Comments were kept concise and focused on explaining important sections of the implementation rather than commenting on every individual line.

---

# 20. GitHub Repository

The completed project is maintained in the following GitHub repository:

`ST10519103/prog7312-2026-prog7312-ice-task-3-iamphineas`

The repository contains the Expo project, corrected `App.tsx`, `README.md`, project configuration files and supporting screenshot assets.

Repository:

**https://github.com/ST10519103/prog7312-2026-prog7312-ice-task-3-iamphineas**

---

# 21. References

Android Developers, 2026. *Android Developers Documentation*. [online] Available at: https://developer.android.com/ [Accessed 12 October 2026].

Expo, 2026. *Expo Documentation*. [online] Available at: https://docs.expo.dev/ [Accessed 12 October 2026].

GitHub, 2026. *GitHub Documentation*. [online] Available at: https://docs.github.com/ [Accessed 12 October 2026].

Meta, 2026. *React Native Documentation*. [online] Available at: https://reactnative.dev/docs/getting-started [Accessed 12 October 2026].

React Native Community, 2026. *React Native Picker*. [online] Available at: https://github.com/react-native-picker/picker [Accessed 12 October 2026].

TypeScript, 2026. *TypeScript Documentation*. [online] Available at: https://www.typescriptlang.org/docs/ [Accessed 12 October 2026].

PROG7312, 2026. *ICE Task 3 – Album Collection & Debugging*. Unpublished coursework document. The Independent Institute of Education (The IIE).

---

# 22. AI Usage Declaration

AI assistance was used during the development and debugging of this task.

The AI tool used was **ChatGPT by OpenAI**.

AI assistance was used for:

- Understanding the supplied React Native and TypeScript code.
- Identifying potential programming and logic errors.
- Explaining TypeScript type mismatches.
- Explaining state management and array operations.
- Assisting with debugging the Picker implementation.
- Suggesting corrections to validation logic.
- Assisting with testing procedures.
- Reviewing the application behaviour.
- Assisting with the structure and wording of the README documentation.

The AI-generated suggestions were **reviewed, tested and verified by the student**. Changes were not accepted solely because they were suggested by the AI. The application was executed in the institutional VM using BlueStacks 5 and Expo Go, and the corrected functionality was manually tested.

The student remains responsible for the final code, testing, documentation and submitted work.

---

# 23. Final Verification Checklist

Before submission, the following requirements were checked:

- [x] Supplied `App.tsx` was examined.
- [x] Application was run before corrections were completed.
- [x] Errors were investigated.
- [x] Errors were corrected.
- [x] Album title validation works.
- [x] Artist validation works.
- [x] Year validation works.
- [x] Genre selection works.
- [x] Rating validation works.
- [x] Valid album information can be added.
- [x] Multiple albums can be stored.
- [x] Albums are displayed using `FlatList`.
- [x] Albums display their stored information.
- [x] Albums can be deleted.
- [x] Deleting one album does not remove the remaining albums.
- [x] The application continues working after deletion.
- [x] The application was tested using BlueStacks 5.
- [x] The application was tested using Expo Go.
- [x] README contains an error log.
- [x] README contains testing information.
- [x] README contains references.
- [x] README contains an AI usage declaration.
- [ ] Completed application screenshot added to `screenshots/album-collection.png`.
- [ ] Final project pushed to GitHub.
- [ ] GitHub repository URL submitted through the required submission platform.

---

# 24. Conclusion

ICE Task 3 provided practical experience in investigating and debugging an existing React Native application. Instead of creating a new application from scratch, the supplied Album Collection application was examined, tested and corrected.

The debugging process demonstrated the importance of understanding TypeScript types, logical conditions, React state, arrays, list rendering, form validation and user interaction. Testing the application through multiple scenarios was particularly important because several problems only became clear when adding multiple albums or attempting to delete an album.

After the corrections, the Album Collection application successfully accepts valid album information, rejects invalid information, stores multiple albums, displays the collection using `FlatList`, allows individual albums to be removed and continues functioning after records have been added or deleted.

The task therefore strengthened both programming and debugging skills and provided practical experience in identifying the difference between compile-time, logic, state-management, dependency and runtime problems.

# PURPLE — Round 2 Submission

## 1. Team Name
Celtics



## 2. Problem Statement & Solution Description

**Problem Statement:**

Friends frequently struggle to track shared group expenses accurately during trips or outings, leading to confusing multi-person repayments. Even after debts are calculated, people often feel awkward repeatedly asking friends to return small amounts of money, causing delayed or forgotten settlements.

**Proposed Solution:**

**FairSplit – MomPay** is a native Android application (Kotlin + Jetpack Compose + Material 3) with a dual personality that solves both sides of group expense friction completely offline:
1. **FairSplit (Smart Fintech Ledger):** Tracks squad expenses, persists data locally with `SharedPreferences`, and runs an exact integer-paise **Minimum Cash Flow** greedy algorithm to reduce messy group repayments into the minimum number of transfers.
2. **MomPay (Satirical Maternal Escalation):** Turns awkward payment reminders into a humorous two-phone escalation workflow—allowing a sender (Phone A) to prepare a real carrier SMS (`MOMPAY1:` Base64URL payload via Android's native `ACTION_SENDTO` composer) to a debtor's mother (Phone B), who pastes it into **Mom Receiver Mode** to trigger a simulated incoming call with a personalized Android `TextToSpeech` reminder.



## 3. Selected Features

### Feature 1: Smart Settlement Engine (Minimum Cash Flow Algorithm & Expense Management)

FairSplit provides full offline group expense tracking and an exact **Minimum Cash Flow** settlement engine (`SettlementCalculator` and `ExpenseCalculator`):
- Uses **64-bit integer `Long` paise arithmetic** (no floating-point rounding drift) with deterministic remainder distribution across participants.
- Supports adding new expenses (with title, rupee amount, payer selection, participant multi-select, **"Split Equally"**, and input validation), deleting expenses, and restoring the preloaded **Goa Trip – Squad** dataset via **Reset Demo**.
- Dynamically computes each member's total paid, total share, net balance, a **Before vs. After** repayment comparison, settlement progress (`₹0` remaining unsettled), and optimized transfer cards.

### Feature 2: Two-Phone SMS-Based MomPay Escalation & Simulated Voice Call

MomPay enables a live two-phone demonstration using standard carrier SMS without requiring internet, cloud backends, or sensitive Android permissions:
- **Phone A (Sender):** Saves Mother's name and Indian mobile number locally (without requesting `READ_CONTACTS`), tracks a 24-hour grace period (plus a **Demo Mode** overdue toggle), and launches the system SMS app via `Intent.ACTION_SENDTO` (`smsto:`) with a `MOMPAY1:<BASE64URL>` invitation token prefilled. Includes an explicit **"I HAVE SENT THE SMS"** sender confirmation.
- **Phone B (Receiver):** **Mom Receiver Mode** lets the receiver paste the SMS from clipboard, extracts and validates the `MOMPAY1:` payload (checking version, required fields, positive amount, and expiry), previews the details, and—only upon explicit **ACCEPT MOMPAY CALL**—displays a **SIMULATED AI VOICE CALL** screen with default ringtone/vibration and Android `TextToSpeech` (`en-IN` with default locale fallback) plus **MUTE / UNMUTE**, **REPLAY**, and **END CALL** controls.



## 4. Setup & Running Instructions

### Prerequisites
- **Android Studio** (Ladybug or newer) with **Android SDK Platform 36** (`minSdk = 26`, `targetSdk = 36`) and **JDK 11+**.
- For the two-phone live demonstration: **two physical Android phones** (Android 8.0 / API 26+) with SIM cards / carrier SMS enabled. (No Wi-Fi, internet, Firebase, or API keys are required.)

### Build & Run Locally
1. Clone or unzip the project repository and open it in **Android Studio**.
2. Wait for Gradle sync to finish (all dependencies are standard AndroidX, Material 3, Jetpack Compose, and Coroutines—no external API keys or `local.properties` secrets are needed).
3. To build the debug APK from the terminal:
   ```bash
   gradle :app:assembleDebug

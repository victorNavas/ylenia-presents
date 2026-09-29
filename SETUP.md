# Firebase setup

The Firebase project and its web app are already created: [ylenia-presents-2026](https://console.firebase.google.com/project/ylenia-presents-2026/overview). The public web SDK configuration is in `index.html`; it is not a private credential. Do not add service-account keys or other private credentials to this repository.

## Firebase project status

The default Firestore database has been created in `eur3`, anonymous authentication is enabled, and the reservation rules are deployed.

## Before publishing on GitHub Pages

1. In Firebase Console, open **Authentication > Settings > Authorized domains** and add the GitHub Pages host (for example, `your-account.github.io`). Local testing works on `localhost`; the published host must be authorized before reservations will work there.
2. Publish `index.html` with GitHub Pages.

To redeploy the reservation rules after changing them, run:

   ```sh
   firebase deploy --only firestore:rules --project ylenia-presents-2026
   ```

The account transfer details are intentionally visible on the public page.

## Gift reservations

The list uses anonymous Firebase sign-in, so visitors do not need to create an account or provide their name. A visitor can reserve an available gift, cancel their own reservation, or mark their own reservation as purchased. Everyone sees status changes in real time. The same browser should be used to manage a reservation, since its anonymous identity is stored there.

`firestore.rules` permits public reads of the twelve known gift statuses, but restricts writes to valid reserve, cancel, and purchase transitions. It does not allow deleting gift records. The app's Firebase API key is public by design; Firestore security rules, not the key, protect the data.

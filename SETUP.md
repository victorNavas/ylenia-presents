# Firebase setup

The Firebase project and its web app are already created: [ylenia-presents-2026](https://console.firebase.google.com/project/ylenia-presents-2026/overview). The public web SDK configuration is in `index.html`; it is not a private credential. Do not add service-account keys or other private credentials to this repository.

## Firebase project status

The default Firestore database has been created in `eur3`, anonymous authentication is enabled, and the reservation rules are deployed.

## Hosting

The public site is hosted on Firebase at <https://ylenia-presents-2026.web.app>. GitHub is the source-code repository; GitHub Pages is disabled to avoid maintaining two live copies.

To publish a site update, run:

   ```sh
   firebase deploy --only hosting --project ylenia-presents-2026
   ```

To redeploy the reservation rules after changing them, run:

   ```sh
   firebase deploy --only firestore:rules --project ylenia-presents-2026
   ```

The account transfer details are intentionally visible on the public page.

## Gift reservations

The list uses anonymous Firebase sign-in, so visitors do not need to create an account or provide their name. A visitor can reserve an available gift, cancel their own reservation, or mark their own reservation as purchased. Everyone sees status changes in real time. The same browser should be used to manage a reservation, since its anonymous identity is stored there.

`firestore.rules` permits public reads of the fourteen known gift statuses, but restricts writes to valid reserve, cancel, and purchase transitions. It does not allow deleting gift records. The app's Firebase API key is public by design; Firestore security rules, not the key, protect the data.

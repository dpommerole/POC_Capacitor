<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png">
  </div>
</template>

<script>

import {
    Plugins
  } from '@capacitor/core'

const { PushNotifications } = Plugins

export default {
  name: 'home',
  components: {
  },
  created () {
    PushNotifications.register()

    // On succcess, we should be able to receive notifications
    PushNotifications.addListener('registration',
      (token) => {
        alert('Push registration success, token: ' + token.value);
      }
    );

    // Some issue with our setup and push will not work
    PushNotifications.addListener('registrationError',
      (error) => {
        alert('Error on registration: ' + JSON.stringify(error));
      }
    );

    // Show us the notification payload if the app is open on our device
    PushNotifications.addListener('pushNotificationReceived',
      (notification) => {
        alert('Push received: ' + JSON.stringify(notification));
      }
    );

    // Method called when tapping on a notification
    PushNotifications.addListener('pushNotificationActionPerformed',
      (notification) => {
        alert('Push action performed: ' + JSON.stringify(notification));
      }
    );
  }
}
</script>

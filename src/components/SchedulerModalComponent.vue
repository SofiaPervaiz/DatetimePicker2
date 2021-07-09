<template>
  <div v-if="showModal">
    <a class="scheduler-exit" id="scheduler-exit" v-on:click="toggleModal"
      >&#x2715;</a
    >
    <div id="scheduler-main">
      <h1>Get Your Questions Answered Now!</h1>
      <p>
        Have you ever wanted to ask a question about one of our services, but
        didn't know how? Schedule a quick call with a VIP Specialist who can
        help you.
      </p>

      <div>
        <ul>
          <li>e</li>
        </ul>
      </div>

      <form id="LeadGen">
        <input
          id="MultivariateId"
          name="MultivariateId"
          type="hidden"
          value="1049649"
          style="display: none"
        />

        <input
          id="NotSaveSignup"
          name="NotSaveSignup"
          type="hidden"
          value="False"
          style="display: none"
        />

        <input
          id="FirstName"
          name="FirstName"
          placeholder="First Name"
          maxlength="20"
          type="text"
          required
        />

        <input
          id="LastName"
          name="LastName"
          placeholder="Last Name"
          maxlength="30"
          type="text"
          required
        />

        <input
          name="email"
          maxlength="50"
          placeholder="Email"
          type="text"
          id="email"
        />

        <input
          id="PhoneNumber"
          name="PhoneNumber"
          placeholder="Phone Number: (555) 555-5555"
          maxlength="14"
          type="text"
          required
        />

        <Date />

        <p>
          We value your
          <a href="http://oxfordclub.com/privacy-policy/" target="_blank"
            >privacy</a
          >.
        </p>
      </form>
    </div>
    <div class="scheduler-confirmation">
      <div class="circle-loader">
        <div class="checkmark draw"></div>
      </div>
      <br />
      <p class="confirmation-message"></p>
    </div>
  </div>
</template>

<script>
import Date from "./DatePickerComponent.vue";

export default {
  name: "SchedulerModal",
  components: {
    Date,
  },
  props: {
    showModal: Boolean,
    toggleModal: Function,
  },
};
</script>
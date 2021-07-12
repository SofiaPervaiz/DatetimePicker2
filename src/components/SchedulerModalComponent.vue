<template>

<div v-if="showModal" class="modal">

  <div  class="scheduler-container" >

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

      <div id="error" v-if="errorMessages.length">
          <ul>
              <li v-for="e in errorMessages" v-bind:key="e.id">{{e}}</li>
          </ul>
      </div>

      <form id="LeadGen" @submit.prevent="processForm">

        <input 
          id="FirstName" 
          name="FirstName" 
          placeholder="First Name" 
          maxlength="20" type="text" 
          v-model="FirstName" 
          required 
          />

        <input
          id="LastName"
          name="LastName"
          placeholder="Last Name"
          maxlength="30"
          type="text"
          v-model="LastName" 
          required
        />

        <input
          name="email"
          maxlength="50"
          placeholder="Email"
          type="text"
          v-model="email"
          id="email"
        />

        <input
          id="PhoneNumber"
          name="PhoneNumber"
          placeholder="Phone Number: (555) 555-5555"
          maxlength="14"
          type="text"
          v-model="PhoneNumber"
          v-on:keyup="formatPhone()"
          required
        />

        <Date />

          <input name="submit" type="submit" value="SUBMIT" class="continue" />

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
</div>
  
</template>

<script>
import Date from "./DatePickerComponent.vue";

export default {
  name: "SchedulerModal",
  data: function data() {
          return {
              FirstName: '',
              LastName: '',
              email: '',
              PhoneNumber: '',
              bestTimeToCall: '',
              errorMessages: []
          };
      },
  components: {
    Date,
  },
  props: {
    showModal: Boolean,
    toggleModal: Function,
    // formatPhone: Function,
  },
   methods: {

     formatPhone() {
       console.log('phone value:  '  + this.PhoneNumber);
       let val = this.PhoneNumber;
       this.PhoneNumber = val.replace(/\D/g, '').replace(/(\d{1,3})(\d{1,3})?(\d{1,4})?/g, function(txt, f, s, t) {
            if (t) {
                return `(${f}) ${s}-${t}`;
            } else if (s) {
                return `(${f}) ${s}`;
            } else if (f) {
                return `(${f})`;
            }
        });
     },
 
    processForm: function(e) {
        let multivariateId = '1049649';
        let notSaveSignup = false;

        console.log('Multi Variant ID: ' + multivariateId);
        console.log('Not Save Signup: ' + notSaveSignup);

        console.log('First Name: ' + this.FirstName);
        console.log('Last Name: ' + this.LastName);
        console.log('Email: ' + this.email);
        console.log('Phone Number: ' + this.PhoneNumber);
        console.log('Best Time to Call: ' + this.bestTimeToCall);
        console.log('Formatted Datetime: ' + this.bestTimeToCall);

        let formData = {
            multivariateId: this.value,
            notSaveSignup: this.value,
            firstName: this.FirstName,
            lastName: this.LastName,
            email: this.email,
            phoneNumber: this.PhoneNumber,
            bestTimeToCall: this.bestTimeToCall
        }

        this.errorMessages = validateForm(formData);

        console.log('ERROR: ' + this.errorMessages.join('/n'));

        if (this.errorMessages.length > 0) {
            e.preventDefault();
        } else {
            submitForm(formData);
        }
    }
}
};

function validateForm(data) {

    const validRegex = /^[a-zA-Z0-9.!#$%&'*+/=?^_`{|}~-]+@[a-zA-Z0-9-]+(?:\.[a-zA-Z0-9-]+)*$/;

    let messages = [];

    if (data.phoneNumber.length < 10) {
        messages.push('Please enter a valid phone number.');
    }

    if (!data.email.match(validRegex)) {
        messages.push('Please enter a valid email address.');
    }

    return messages;

}

function submitForm(data) {

    const myHeaders = new Headers({
        'Origin': 'https://apps.pubsvs.com',
    });

    const url = 'https://signup.oxfordclub.com/Content/SaveFreeSignups?MultivariateId=' + data.multivariateId + '&oneClick=true&email=' + data.email + '&FirstName=' + data.firstName + '&LastName=' + data.lastName + '&PhoneNumber=' + data.phoneNumber + '&BestTimeToCall=' + data.bestTimeToCall;

    fetch(url, {
            method: 'POST',
            mode: 'no-cors',
            headers: myHeaders
        }).then(function() {
            showConfirmationMessage(data.bestTimeToCall);
        })
        .then(res => console.log(res));
}

function showConfirmationMessage(bestTimeToCall) {

    const schedulerMain = document.getElementById('scheduler-main');
    const confirmation = document.getElementsByClassName('scheduler-confirmation');
    const circleLoader = document.getElementsByClassName('circle-loader');
    const checkmark = document.getElementsByClassName('checkmark');
    const confirmationMessage = document.getElementsByClassName('confirmation-message');
    const time = bestTimeToCall.toLocaleString('en-US', { hour: 'numeric', minute: 'numeric' });


    schedulerMain.style.display = "none";
    confirmation[0].style.display = "block";
    circleLoader[0].classList.toggle('load-complete');
    checkmark[0].style.display = "block";
    confirmationMessage[0].innerHTML = "Thank you for scheduling a time with one of our VIP specialists. Get your questions ready! We are excited to help you in any way that you can. Your call is reserved for " + time + ' on ' + getMonthName(bestTimeToCall.getMonth()) + ' ' + bestTimeToCall.getDate();


}


function getMonthName(month) {
    const monthNames = ["January", "February", "March", "April", "May", "June",
        "July", "August", "September", "October", "November", "December"
    ];

    return monthNames[month];
}
</script>
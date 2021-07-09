<template>
  <date-picker
    locale="en"
    v-model="datetime"
    format="YYYY-MM-DD HH:mm"
    type="datetime"
    :jumpMinute="15"
    :roundMinute="true"
    :disable="[
      'Saturday',
      'Sunday',
      /(.*)01:(.*)/,
      /(.*)02:(.*)/,
      /(.*)03:(.*)/,
      /(.*)04:(.*)/,
      /(.*)05:(.*)/,
      /(.*)06:(.*)/,
      /(.*)07:(.*)/,
      /(.*)18:(.*)/,
      /(.*)19:(.*)/,
      /(.*)20:(.*)/,
      /(.*)21:(.*)/,
      /(.*)22:(.*)/,
      /(.*)23:(.*)/,
    ]"
    :color="colors[activeColorIndex]"
    :show="show"
    @close="show = false"
  />
</template>

<script>
import DatePicker from "vue-datetime-js";

export default {
  name: "Date",
  components: {
    DatePicker,
  },
  data() {
    return {
      datetime: "",
      show: false,
      colors: [
        "#5c6bc0",
        "#e91e63",
        "#7b1fa2",
        "#1e88e5",
        "#03a9f4",
        "#00acc1",
        "#ff9800",
        "dimgray",
      ],
      activeColorIndex: 4,
    };
  },
};
</script>

<template>
  <pre class="text-white font-bold">
 __| |____________________________________________| |__
(__   ____________________________________________   __)
   | |                                            | |  
   | |   {{ paddedName }}| |
   | |                                            | |
   | |   {{ paddedDescription }}| |
   | |                                            | |
   | |                                            | |
   | |                                            | |
 __| |____________________________________________| |__
(__   ____________________________________________   __)
   | |                                            | |                                 
  </pre>
</template>

<script>
export default {
  name: "Tutorials",
  props: {
    name: {
      type: String,
      required: true,
    },
    description: {
      type: String,
      required: true,
    },
  },
  computed: {
    paddedName() {
      return this.name.padEnd(41);
    },
    paddedDescription() {
      return this.description.padEnd(41);
    },
  },
};
</script>

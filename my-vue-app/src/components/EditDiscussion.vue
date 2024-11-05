<template>
    <div class="container mt-5">
      <h2 class="text-center mb-4">CHOOSE YOUR VOTE</h2>
      <b-card class="p-4 shadow">
        <form @submit.prevent="updateDiscussion">

          <div>
            <p class="votee">IF YOU LIKE THIS EVENT , VOTE YES BY CLICKING ON THE CHECKBOX:</p>
            <input type="checkbox" label="Yes" v-model="form.status"> I agree to vote on this event.
    
          </div>
  
          <b-button variant="primary" type="submit" class="w-100 mt-3 rounded-pill">
            SAVE VOTE
          </b-button>
        </form>
        <router-link to="/discussions" class="btn btn-secondary w-100 mt-2 rounded-pill">
          Cancel
        </router-link>
      </b-card>
    </div>
  </template>
  
  <script>
  import { getFirestore, doc, getDoc, updateDoc } from 'firebase/firestore';
  import { useRouter } from 'vue-router';
  
  const db = getFirestore();
  
  export default {
    data() {
      return {
        title: '',
        content: '',
        form: {
        status: 0 
      }
      };
      
    },

    computed: {
    statusNumber() {
      return this.form.status ? 1 : 0;
    }
  },
    async mounted() {
      const discussionId = this.$route.params.id;
      const docRef = doc(db, 'discussions', discussionId);
      const docSnap = await getDoc(docRef);
      if (docSnap.exists()) {
        const discussion = docSnap.data();
        this.title = discussion.title;
        this.content = discussion.content;
        this.votes = discussion.votes;
      } else {
        console.log('No such document!');
      }
    },
    methods: {
      async updateDiscussion() {
        const discussionId = this.$route.params.id;
        try {
          await updateDoc(doc(db, 'discussions', discussionId), {
            title: this.title,
            content: this.content,
            votes:this.votes + this.form.status ,
            
          });
          this.$router.push('/discussions'); // Redirect back to discussions list
        } catch (error) {
          console.error('Error updating discussion:', error);
          alert('Failed to update discussion');
        }
      },
    },
  };
  </script>
  
  <style scoped>
  .container {
    max-width: 800px; /* Center the container */
    margin: auto; /* Center the content */
  }
  
  h2 {
    color: #ff5e62; /* Title color */
    font-weight: bold; /* Bold title */
    font-size: xx-large; /* Increase title size */
  }
  .votee {
    color: rgb(51, 51, 51); /* Title color */
    font-weight: bold; /* Bold title */
    font-size: large; /* Increase title size */
  }
  
  .b-card {
    border-radius: 15px; /* Rounded corners for the card */
    background-color: #f9f9f9; /* Light background for the card */
    box-shadow: 0 4px 20px rgba(0, 0, 0, 0.1); /* Subtle shadow */
  }
  
  .b-form-input, .b-form-textarea {
    border-radius: 20px; /* Rounded corners for inputs */
    border: 1px solid #ced4da; /* Light border color */
  }
  
  .b-button {
    background-color: #ff5e62; /* Bootstrap primary color */
    color: white; /* Text color */
    font-weight: bold; /* Bold text */
  }
  
  .b-button:hover {
    background-color: #ff5e62; /* Darker blue on hover */
  }
  
  .router-link {
    text-decoration: none; /* Remove underline */
    margin-top: 10px; /* Space above cancel button */
  }
  </style>
  
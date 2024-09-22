<script setup>
import { ref } from 'vue';

const showModal = ref(false);
const settings = ref(false);
const changing = ref(false);
const showDiv = ref(false);
const form = ref({
  firstName: 'Ilias',
  lastName: 'Nyssanbek',
  dob: '17-11-2004',
  country: 'Kazakhstan',
  city: 'Almaty',
  gender: '',
});

// Store the current password
const currentPassword = ref('Aa123%');

const errors = ref({
  firstName: '',
  lastName: '',
  dob: '',
  country: '',
  city: '',
  gender: '',
});

const passwordForm = ref({
  oldPassword: '',
  newPassword: '',
  confirmPassword: '',
});

const passwordErrors = ref({
  oldPassword: '',
  newPassword: '',
  confirmPassword: '',
});

const validatePasswordForm = () => {
  let valid = true;

  passwordErrors.value = {
    oldPassword: '',
    newPassword: '',
    confirmPassword: '',
  };

  if (!passwordForm.value.oldPassword) {
    passwordErrors.value.oldPassword = 'Old password is required';
    valid = false;
  }

  if (passwordForm.value.oldPassword !== currentPassword.value) {
    passwordErrors.value.oldPassword = 'Old password is incorrect';
    valid = false;
  }

  if (!passwordForm.value.newPassword) {
    passwordErrors.value.newPassword = 'New password is required';
    valid = false;
  }

  if (passwordForm.value.newPassword !== passwordForm.value.confirmPassword) {
    passwordErrors.value.confirmPassword = 'Passwords do not match';
    valid = false;
  }

  return valid;
};

const handlePasswordChange = () => {
  if (validatePasswordForm()) {
    // Update the current password
    currentPassword.value = passwordForm.value.newPassword;
    changing.value = false; 
    // Clear the password form fields
    passwordForm.value.oldPassword = '';
    passwordForm.value.newPassword = '';
    passwordForm.value.confirmPassword = '';
  } 
};

const validateForm = () => {
  let valid = true;

  errors.value = {
    firstName: '',
    lastName: '',
    dob: '',
    country: '',
    city: '',
    gender: '',
  };

  if (!form.value.firstName) {
    errors.value.firstName = 'First name is required';
    valid = false;
  }

  if (!form.value.lastName) {
    errors.value.lastName = 'Last name is required';
    valid = false;
  }

  const dobRegex = /^\d{2}-\d{2}-\d{4}$/;
  if (!dobRegex.test(form.value.dob)) {
    errors.value.dob = 'Date of birth must be in format DD-MM-YYYY';
    valid = false;
  }

  if (!form.value.country) {
    errors.value.country = 'Country is required';
    valid = false;
  }

  if (!form.value.city) {
    errors.value.city = 'City is required';
    valid = false;
  }

  return valid;
};

const handleSubmit = () => {
  if (validateForm()) {
    showModal.value = false; 
  }
};

const formNumerology = ref({
  nameSurname: '',
  dob: '',
});

const errorsNumerology = ref({
  nameSurname: '',
  dob: '',
});

const handleNumerologySubmit = () => {
  if (formNumerology.value.nameSurname && formNumerology.value.dob) {
    showDiv.value = false; 
  } else {
    if (!formNumerology.value.nameSurname) {
      errorsNumerology.value.nameSurname = 'Name and surname are required.';
    }
    if (!formNumerology.value.dob) {
      errorsNumerology.value.dob = 'Date of birth is required.';
    }
  }
};
</script>



<template class="bg-[#F3F6FA] w-[100%] h-[100%] ">
<link href='https://fonts.googleapis.com/css?family=Montserrat' rel='stylesheet'>
    <header>
     <div class="flex space-x-[19%] mt-[30px] ml-[25px]">
      <div>
           <img src="./images/logo_full (1) 1.svg" alt="" class="max-[767px]:w-[150px]">
      </div>
      <div class="flex space-x-[123px] max-[767px]:hidden">
           <h1 class="text-[20px] font-[400]">Home</h1>
           <h1 class="text-[20px]">About</h1>
           <h1 class="text-[20px]">Help</h1>         
      </div>
      <div class="bg-[#31CA85] w-[315px] h-[70px] flex items-center justify-center rounded-[10px] space-x-[20px] drop-shadow-lg  
      mt-[-20px] pl-[2%] max-[767px]:hidden" >
            <h1 class="text-[#ffffff] text-[12px]">ilias2004nyssanbek@gmail.com</h1>
             <div class="flex justify-end">
              <img src="/src/images/КРАШ.jpg" alt="" class=" w-[50px] h-[50px] rounded-[50%] ml-[30px]">
             </div>
      </div>        
     </div>
  </header>
  <main class="flex justify-center mt-[4%]">
      <div class="w-[1005px] h-[645px] md:drop-shadow-lg  rounded-[10px] bg-[#FFFFFF] ">
          <div class="flex items-center md: space-x-[65%] max-[767px]:space-x-[30%]">
            <div>
               <h1 class="text-[33px] font-[700] mt-[30px] md:ml-[40px] max-[767px]:ml-[130%]">Profile</h1>
            </div>
            <div class="flex md: mt-[3%] max-[767px]:mt-[-37%] space-x-[20px] max-[767px]:ml-[300px]">
              <button @click="showModal = true" class="md:w-[110px] md:h-[37px] border-[2px] rounded-[32px] mt-[2%]  
              max-[767px]:w-[88px] max-[767px]:h-[31px] max-[767px]:ml-[5%] gradient-button">Edit</button>
              <img src="./images/gear.png" alt=""  @click="settings=true" class="md:w-[50px] max-[767px]:w-[38px] max-[767px]:ml-[25%]">
            </div>
             <div v-if="showModal" class="fixed flex items-center justify-center">
    <div class="bg-white rounded-lg p-5 md:w-[1005px] max-[767px]:w-[350px] h-[680px] mt-[518px] md:ml-[-653px] max-[767px]:ml-[-100px]">
      <h2 class="font-bold text-[33px]">Editing Profile</h2>

      <div class="flex flex-col justify-center items-center space-y-[20px] mt-[10%]">
        <div class="border-[#000000] border-[1px] rounded-[12px] md:w-[650px] max-[767px]:w-[350px] h-[36px] pl-[15px] flex items-center">
          <input v-model="form.firstName" type="text" placeholder="First name" class="w-full">
        </div>
        <span class="text-red-500 text-sm">{{ errors.firstName }}</span>

        <div class="border-[#000000] border-[1px] rounded-[12px] md:w-[650px] max-[767px]:w-[350px] h-[36px] pl-[15px] flex items-center">
          <input v-model="form.lastName" type="text" placeholder="Last name" class="w-full">
        </div>
        <span class="text-red-500 text-sm">{{ errors.lastName }}</span>

        <div class="border-[#000000] border-[1px] rounded-[12px] md:w-[650px] max-[767px]:w-[350px] h-[36px] pl-[15px] flex items-center">
          <input v-model="form.dob" type="text" placeholder="Date of Birth (DD-MM-YYYY)" class="w-full">
        </div>
        <span class="text-red-500 text-sm">{{ errors.dob }}</span>


        <div class="border-[#000000] border-[1px] rounded-[12px] md:w-[650px] max-[767px]:w-[350px] h-[36px] pl-[15px] flex items-center">
          <input v-model="form.country" type="text" placeholder="Country" class="w-full">
        </div>
        <span class="text-red-500 text-sm">{{ errors.country }}</span>


        <div class="border-[#000000] border-[1px] rounded-[12px] md:w-[650px] max-[767px]:w-[350px] h-[36px] pl-[15px] flex items-center">
          <input v-model="form.city" type="text" placeholder="City" class="w-full">
        </div>
        <span class="text-red-500 text-sm">{{ errors.city }}</span>

        <div class="border-[#000000] border-[1px] rounded-[12px] md:w-[650px] max-[767px]:w-[350px] h-[36px] pl-[15px] flex items-center space-x-5">
           <select name="" id="" v-model="form.gender">
            <option value="">Male</option>
            <option value="">Female</option>
           </select>
        </div>
        <span class="text-red-500 text-sm">{{ errors.gender }}</span>
      </div>

      <div class="flex max-[767px]:flex-col max-[767px]:items-center justify-center max-[767px]:space-y-4 md:space-x-[10px] md:mt-[3%] max-[767px]:mt-[6%]">
        <button @click="handleSubmit" class="w-[110px] h-[37px] border-[2px] rounded-[32px] mt-[2%] bg-[#1531B0] text-[#FFFFFF]">Finish</button>
        <button @click="showModal = false" class="w-[110px] h-[37px] border-[2px] rounded-[32px] mt-[2%] bg-[#31CA85] text-[#FFFFFF] ">Cancel</button>
      </div>
    </div>
  </div>
           <div v-if="settings" class="fixed ">
              <div class="bg-white rounded-lg p-5 w-[305px] h-[190px] drop-shadow-lg">
                  <div class="flex justify-center"><h1>Setting the parameters</h1></div>
                  <div class="flex justify-center"><button class="rounded-[32px] border-[1px] border-[#1531B0] text-[#1531B0] 
                  h-[40px] w-[220px] mt-[10px] " @click="changing=true">Change the password</button></div>
                  <div v-if="changing" class="fixed">
                   <div class="bg-white rounded-lg p-5 md:w-[1005px] h-[600px] max-[767px]:w-[350px] md:ml-[-67%] max-[767px]:ml-[-33%] mt-[-5%]">
                      <h2 class=" font-bold text-[33px]">Changing password</h2>
                      <div class="flex flex-col space-y-[20px] mt-[15%]">
                        <div class="flex justify-center">
                           <input v-model="passwordForm.oldPassword" type="password" class="border-[#000000] border-[1px] rounded-[12px] w-[650px] h-[36px] pl-[15px] flex items-center" placeholder="Write your old password...">
                        </div>
                        <span class="text-red-500 text-sm">{{ passwordErrors.oldPassword }}</span>
      
                        <div class="flex justify-center">
                            <input v-model="passwordForm.newPassword" type="password" class="border-[#000000] border-[1px] rounded-[12px] w-[650px] h-[36px] pl-[15px] flex items-center" placeholder="Write your new password...">
                        </div>
                        <span class="text-red-500 text-sm">{{ passwordErrors.newPassword }}</span>
      
                      <div class="flex justify-center">
                         <input v-model="passwordForm.confirmPassword" type="password" class="border-[#000000] border-[1px] rounded-[12px] w-[650px] h-[36px] pl-[15px] flex items-center" placeholder="Repeat the password...">
                      </div>
                      <span class="text-red-500 text-sm">{{ passwordErrors.confirmPassword }}</span>
                      </div>
                      <div class="flex max-[767px]:flex-col max-[767px]:items-center justify-center max-[767px]:space-y-4 md:space-x-[20px] mt-[3%]">
                        <button @click="handlePasswordChange" class="w-[110px] h-[37px] border-[2px] rounded-[32px] mt-[2%] bg-[#1531B0] text-[#FFFFFF]">Finish</button>
                         <button @click="changing = false" class="w-[110px] h-[37px] border-[2px] rounded-[32px] mt-[2%] bg-[#31CA85] text-[#FFFFFF]">Cancel</button>
                      </div>
                    </div>
                  </div>

                  <div class="flex justify-center"><div class="rounded-[32px] border-[1px] border-[#1531B0] text-[#1531B0] 
                  h-[40px] w-[220px] mt-[10px] flex justify-center items-center">
                    <select name="languages" id="">
                      <option value="">Kazakh</option>
                      <option value="">Russian</option>
                      <option value="">English</option>
                    </select>
                  </div>
                  </div>
                   <div class="flex justify-center"><button @click="settings = false" class=" w-[90px] h-[32px] border-[2px] bg-[#31CA85] text-[#FFFFFF]  
                   rounded-[32px] mt-[2%]">Cancel</button></div>
              </div>
           </div>
          </div>
          <div class="flex flex-col justify-center items-center space-y-[30px] mt-[5%] ">
            <div class="flex justify-between max-[767px]:max-w-[80%] w-full md:max-w-md">
              <h1 class="text-[16px] font-light">Name</h1>
              <h1 class="text-[16px] ">{{form.firstName}}</h1>
            </div>
            <div class="flex justify-between max-[767px]:max-w-[80%] w-full md:max-w-md">
               <h1 class="text-[16px] font-light">Surname</h1>
               <h1 class="text-[16px] ">{{form.lastName}}</h1>
            </div>
            <div class="flex justify-between max-[767px]:max-w-[80%] w-full md:max-w-md">
              <h1 class="text-[16px] font-light">Date of birth</h1>
              <h1 class="text-[16px] ">{{form.dob}}</h1>
            </div>
            <div class="flex justify-between max-[767px]:max-w-[80%] w-full md:max-w-md">
               <h1 class="text-[16px] font-light">Phone number</h1>
               <h1 class="text-[16px] ">8-775-199-21-57</h1>
            </div>
            <div class="flex justify-between max-[767px]:max-w-[80%] w-full md:max-w-md">
              <h1 class="text-[16px] font-light">Email</h1>
              <h1 class="text-[14px] ">ilias2004nyssanbek@gmail.com</h1>
            </div>
            <div class="flex justify-between max-[767px]:max-w-[80%] w-full md:max-w-md">
               <h1 class="text-[16px] font-light">Gender</h1>
               <h1 class="text-[16px] ">Male</h1>
            </div>
            <div class="flex justify-between max-[767px]:max-w-[80%] w-full md:max-w-md">
              <h1 class="text-[16px] font-light">Country</h1>
              <h1 class="text-[16px] ">{{form.country}}</h1>
            </div>
            <div class="flex justify-between max-[767px]:max-w-[80%] w-full md:max-w-md">
               <h1 class="text-[16px] font-light">City/Region</h1>
               <h1 class="text-[16px] ">{{form.city}}</h1>
            </div>
            <div class="flex justify-between max-[767px]:max-w-[80%] w-full md:max-w-md">
               <h1 class="text-[16px] font-light">Password</h1>
               <h1 class="text-[16px] ">{{currentPassword}}</h1>
            </div>
            <div class="flex space-x-1">
               <a class="text-[14px] text-[#31CA85]">Want to fill  the numerology report?</a>
               <input type="checkbox" @change="showDiv = $event.target.checked">
            </div>
             <div v-if="showDiv" class="fixed">
               <div class="bg-white rounded-lg p-5 w-[305px] h-[190px] drop-shadow-lg flex flex-col items-center space-y-[15px] justify-center mt-[-40px]">
                <div class="flex justify-center">
                  <h1>Numerology subscription</h1>
                </div>

                <input
                  v-model="formNumerology.nameSurname"
                  class="border-[1px] border-[#B3B3BC] w-[220px] h-[40px] rounded-[32px] placeholder-[12px] pl-[10px]"
                  placeholder="Name, surname.."
                />
                <span class="text-red-500 text-sm">{{ errorsNumerology.nameSurname }}</span>
                <input
                    v-model="formNumerology.dob"
                    class="border-[1px] border-[#B3B3BC] w-[220px] h-[40px] rounded-[32px] placeholder-[12px] pl-[10px]"
                    placeholder="Date of birth (dd/mm/yy)"
                />
               <span class="text-red-500 text-sm">{{ errorsNumerology.dob }}</span>

               <button @click="handleNumerologySubmit" class="w-[110px] h-[37px] border-[2px] rounded-[32px] mt-[2%] gradient-button">Send</button>
              </div>
             </div>
          </div>

      </div>
  </main>



</template>

<style scoped>

*{
  font-family: 'Monserrat',sans-serif;
}
 body {
   background-color: #F3F6FA;
}
button {
    border-image: 'custom-gradient';
    border-radius: 32px;
}
.gradient-button {
    background-image: linear-gradient(to right, #31CA85, #0a287b);
    color: white; /* Change text color to white for contrast */
    border-radius: 32px;
    transition: background 0.3s ease; /* Smooth transition */
}

.gradient-button:hover {
    background-color: transparent; /* Change to transparent on hover */
    color: #31CA85; /* Change text color on hover */
}

</style>

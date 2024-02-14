<script>
$: messages = []
import { collection, addDoc, getDocs } from "firebase/firestore"; 
import { initializeApp } from "firebase/app";
import "firebase/firestore";
import { getFirestore } from "firebase/firestore";

const firebaseConfig = {
	apiKey: "AIzaSyAfffxPdacSeBy8sRC1bi7QdPE6WmHmyvo",
	authDomain: "clown-wall.firebaseapp.com",
	projectId: "clown-wall",
	storageBucket: "clown-wall.appspot.com",
	messagingSenderId: "366308901798",
	appId: "1:366308901798:web:5f393cbb5be6caa425c567",
	measurementId: "G-XVXF9JW36D"
  };

const app = initializeApp(firebaseConfig);
const db = getFirestore(app);



    let inputValue = '';
    
    function handleSubmit() {
        alert('Done!');
    }


    async function addDocument() {
        const docRef = await addDoc(collection(db, "messages"), {
            message: inputValue
        });
        console.log("Document written with ID: ", docRef.id);
        getDocument()
    }


    async function getDocument() {
        const querySnapshot = await getDocs(collection(db, "messages"));
        messages = []; // Remove the old messages array
        querySnapshot.forEach((doc) => {
            const concs = doc.data();
            messages.push(concs); // Instead of setting messages, append to it
        });
    }


    getDocument()
    

</script>

<style>

    * {
        background-color: #69B578;
    }
    .container {
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
        height: 100vh;
        color: #3E000C;
    }
    

    #header {
            position: absolute;
            top: 10px;
            left: 10px;
            font-size: 32px;
            font-weight: bold;
            color: #3E000C;
            margin: 0;
        }
    
    .input-field {
        display: flex;
        align-items: center;
        padding: 10px;
        border: 2px solid #3E000C;
        border-radius: 5px;
        margin-bottom: 10px;
        width: 60vw;
    }
    
    .input-field input {
        flex: 1;
        border: none;
        outline: none;
        font-size: 16px;
        padding: 5px;
    }
    
    .submit-button {
        display: flex;
        align-items: center;
        justify-content: center;
        padding: 10px 20px;
        background-color: #007bff;
        color: #fff;
        border: none;
        border-radius: 5px;
        cursor: pointer;
        font-size: 16px;
    }
    
    .submit-button:hover {
        background-color: #0056b3;
    }
    
    .submit-button::after {
        content: '→';
        margin-left: 5px;
    }
    ul {
        list-style: none;
    }
</style>

<div class="container">
    <div id="header">The Clown's Wall</div>

    <div class="display">
        <ul>
            {#each messages as message}
                <li><h3>Anon>  {message.message}</h3></li>
            {/each}
        </ul>
    </div>
    
    <div class="input-field">
        <input type="text" bind:value={inputValue} placeholder="You are the entire circus." />
    </div>

    
    <button class="submit-button" on:click={addDocument}>Submit</button>
</div>
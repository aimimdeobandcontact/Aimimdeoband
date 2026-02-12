<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title>AIMIM Deoband – Campaign Dashboard</title>

<script src="https://cdn.tailwindcss.com"></script>
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css">

<style>
  body { background:#071a12; }
  .mim-green { background:#008248; }
</style>
</head>

<body class="text-white font-sans">

<!-- NAV -->
<nav class="mim-green p-4 sticky top-0 shadow-lg">
  <div class="max-w-6xl mx-auto flex justify-between items-center">
    <h1 class="font-black text-xl">AIMIM DEOBAND</h1>
    <div class="space-x-5 text-sm font-bold">
      <a href="#join">Join</a>
      <a href="#volunteer">Volunteer</a>
      <a href="#donate">Donate</a>
      <a href="#media">Media</a>
      <a href="#contact">Contact</a>
    </div>
  </div>
</nav>

<!-- HERO + LIVE COUNTER -->
<section class="text-center py-24 bg-gradient-to-b from-green-900 to-black">
  <h2 class="text-5xl font-black mb-4">Majlis Zindabad</h2>
  <p class="mb-8">Official Campaign Dashboard</p>

  <div class="mb-6">
    <p class="text-sm text-gray-300">Total Members Joined</p>
    <h3 id="memberCount" class="text-6xl font-black text-green-400">0</h3>
  </div>

  <a href="#join" class="bg-green-600 px-8 py-4 rounded-xl font-bold hover:bg-green-700">
    JOIN NOW
  </a>
</section>

<!-- COUNTDOWN -->
<section class="py-12 text-center">
  <h3 class="text-3xl font-bold mb-4">Election Countdown</h3>
  <p id="countdown" class="text-4xl text-green-400 font-black"></p>
</section>

<!-- JOIN -->
<section id="join" class="py-16 text-center">
  <h3 class="text-3xl font-bold mb-6">Membership Registration</h3>
  <input id="m_name" placeholder="Name" class="p-3 text-black rounded mb-3">
  <br>
  <button onclick="submitMember()" class="mim-green px-10 py-3 rounded font-bold">
    Join + WhatsApp
  </button>
</section>

<!-- VOLUNTEER -->
<section id="volunteer" class="py-16 text-center bg-black">
  <h3 class="text-3xl font-bold mb-6">Volunteer Registration</h3>
  <input id="v_name" placeholder="Name" class="p-3 text-black rounded mb-2">
  <br>
  <input id="v_phone" placeholder="Phone" class="p-3 text-black rounded mb-2">
  <br>
  <select id="v_role" class="p-3 text-black rounded mb-3">
    <option>Social Media</option>
    <option>Ground Worker</option>
    <option>Event Manager</option>
  </select>
  <br>
  <button onclick="submitVolunteer()" class="mim-green px-10 py-3 rounded font-bold">
    Register Volunteer
  </button>
</section>

<!-- DONATE -->
<section id="donate" class="py-16 text-center">
  <h3 class="text-3xl font-bold mb-6">Support Campaign</h3>
  <input id="d_name" placeholder="Name" class="p-3 text-black rounded mb-2">
  <br>
  <input id="d_amount" placeholder="Amount" class="p-3 text-black rounded mb-3">
  <br>
  <button onclick="submitDonation()" class="mim-green px-10 py-3 rounded font-bold">
    Record Donation
  </button>

  <div class="mt-6">
    <p class="text-green-400 font-bold">UPI ID: aimimdeoband@upi</p>
  </div>
</section>

<!-- MEDIA -->
<section id="media" class="py-16 text-center bg-black">
  <h3 class="text-3xl font-bold mb-6">Rally Media</h3>
  <!-- Replace with your public Google Drive folder embed if needed -->
  <iframe src="https://drive.google.com/embeddedfolderview?id=REPLACE_WITH_DRIVE_FOLDER_ID#grid"
          style="width:90%; height:400px; border:0;"></iframe>
</section>

<!-- WHATSAPP GROUP -->
<section class="py-16 text-center">
  <h3 class="text-3xl font-bold mb-6">Join Official WhatsApp Group</h3>
  <a href="REPLACE_WITH_WHATSAPP_GROUP_LINK" target="_blank"
     class="bg-green-600 px-10 py-4 rounded-xl font-bold inline-block">
     Join WhatsApp Group
  </a>
</section>

<!-- CONTACT -->
<section id="contact" class="py-20 text-center bg-black">
  <h3 class="text-3xl font-bold mb-10 text-green-400">Official Social Media</h3>
  <div class="flex justify-center gap-12 text-5xl">
    <a href="https://instagram.com/faizaliaimim" class="text-pink-500"><i class="fab fa-instagram"></i></a>
    <a href="https://facebook.com/faizaliaimim" class="text-blue-500"><i class="fab fa-facebook"></i></a>
    <a href="https://youtube.com/@faizaliaimim" class="text-red-500"><i class="fab fa-youtube"></i></a>
  </div>
  <p class="mt-8 text-lg">📧 aimimdeobandcontact@gmail.com</p>
</section>

<footer class="text-center py-8 bg-black text-sm text-gray-400">
  Banhara Khas, Deoband, Saharanpur, Uttar Pradesh
</footer>

<script>
const SCRIPT_URL = "REPLACE_WITH_SCRIPT_URL";

// live member counter
fetch(SCRIPT_URL).then(r=>r.text()).then(c=>{
  document.getElementById("memberCount").innerText = c;
});

// membership
function submitMember(){
  const name = document.getElementById("m_name").value;
  fetch(SCRIPT_URL,{method:"POST",body:JSON.stringify({type:"member",name:name})});
  window.location = "https://wa.me/919888183650?text=I want to join AIMIM Deoband. Name: "+name;
}

// volunteer
function submitVolunteer(){
  fetch(SCRIPT_URL,{
    method:"POST",
    body:JSON.stringify({
      type:"volunteer",
      name:v_name.value,
      phone:v_phone.value,
      role:v_role.value
    })
  });
  alert("Volunteer Registered");
}

// donation
function submitDonation(){
  fetch(SCRIPT_URL,{
    method:"POST",
    body:JSON.stringify({
      type:"donation",
      name:d_name.value,
      amount:d_amount.value
    })
  });
  alert("Donation Recorded");
}

// countdown
const electionDate = new Date("May 10, 2026").getTime();
setInterval(()=>{
  const now = new Date().getTime();
  const days = Math.floor((electionDate-now)/(1000*60*60*24));
  document.getElementById("countdown").innerText = days+" Days Left";
},1000);
</script>

</body>
</html>

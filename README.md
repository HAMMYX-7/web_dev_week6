# web_dev_week6
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>JS Event Assignment</title>
  <link rel="stylesheet" href="style.css" />
</head>
<body>
  <header>
    <h1>Interactive Web Page</h1>
  </header>

  <main>
    <!-- Event Handling Section -->
    <section>
      <h2>Event Handling 🎈</h2>
      <button id="clickBtn">Click Me</button>
      <div id="hoverBox">Hover over me!</div>
      <input type="text" id="keyInput" placeholder="Type something..." />
      <button id="secretBtn">Double-Click Me</button>
    </section>

    <!-- Interactive Elements Section -->
    <section>
      <h2>Interactive Elements 🎮</h2>
      <button id="colorBtn">Change My Color</button>

      <div class="gallery">
        <img src="image1.jpg" alt="Image 1" class="gallery-img" />
        <img src="image2.jpg" alt="Image 2" class="gallery-img" />
        <img src="image3.jpg" alt="Image 3" class="gallery-img" />
      </div>

      <div class="tabs">
        <button class="tablink" data-tab="tab1">Tab 1</button>
        <button class="tablink" data-tab="tab2">Tab 2</button>
        <button class="tablink" data-tab="tab3">Tab 3</button>
      </div>
      <div id="tab1" class="tabcontent">Content for Tab 1</div>
      <div id="tab2" class="tabcontent">Content for Tab 2</div>
      <div id="tab3" class="tabcontent">Content for Tab 3</div>
    </section>

    <!-- Form Validation Section -->
    <section>
      <h2>Form Validation 📋✅</h2>
      <form id="signupForm" novalidate>
        <label for="email">Email:</label>
        <input type="email" id="email" required />
        <span id="emailError" class="error"></span>

        <label for="password">Password:</label>
        <input type="password" id="password" required minlength="8" />
        <span id="passwordError" class="error"></span>

        <button type="submit">Submit</button>
      </form>
    </section>
  </main>

  <footer>
    <p>&copy; 2025 Your Name</p>
  </footer>

  <script src="script.js"></script>
</body>
</html>

body {
  font-family: Arial, sans-serif;
  margin: 20px;
}

section {
  margin-bottom: 40px;
}

#hoverBox {
  width: 200px;
  height: 100px;
  background-color: lightgray;
  line-height: 100px;
  text-align: center;
  margin-top: 10px;
}

.gallery {
  display: flex;
  gap: 10px;
  margin-top: 10px;
}

.gallery-img {
  width: 100px;
  height: 100px;
  cursor: pointer;
  transition: transform 0.3s;
}

.gallery-img:hover {
  transform: scale(1.1);
}

.tabs {
  margin-top: 20px;
}

.tablink {
  padding: 10px;
  margin-right: 5px;
  cursor: pointer;
}

.tabcontent {
  display: none;
  margin-top: 10px;
  border: 1px solid #ccc;
  padding: 10px;
}

.error {
  color: red;
  font-size: 0.9em;
  margin-left: 10px;
}

// Event Handling
document.getElementById("clickBtn").addEventListener("click", () => {
  alert("Button clicked!");
});

const hoverBox = document.getElementById("hoverBox");
hoverBox.addEventListener("mouseover", () => {
  hoverBox.style.backgroundColor = "lightblue";
});
hoverBox.addEventListener("mouseout", () => {
  hoverBox.style.backgroundColor = "lightgray";
});

document.getElementById("keyInput").addEventListener("keypress", (e) => {
  console.log(`Key pressed: ${e.key}`);
});

document.getElementById("secretBtn").addEventListener("dblclick", () => {
  alert("Secret action triggered!");
});

// Interactive Elements
document.getElementById("colorBtn").addEventListener("click", function () {
  this.style.backgroundColor = this.style.backgroundColor === "green" ? "blue" : "green";
});

const tabs = document.querySelectorAll(".tablink");
const tabContents = document.querySelectorAll(".tabcontent");

tabs.forEach((tab) => {
  tab.addEventListener("click", () => {
    tabContents.forEach((content) => (content.style.display = "none"));
    document.getElementById(tab.dataset.tab).style.display = "block";
  });
});

// Form Validation
const emailInput = document.getElementById("email");
const passwordInput = document.getElementById("password");
const emailError = document.getElementById("emailError");
const passwordError = document.getElementById("passwordError");

function validateEmail(email) {
  const emailRegex = /^[^\\s@]+@[^\\s@]+\\.[^\\s@]+$/;
  return emailRegex.test(email);
}

emailInput.addEventListener("input", () => {
  if (!validateEmail(emailInput.value)) {
    emailError.textContent = "Please enter a valid email.";
  } else {
    emailError.textContent = "";
  }
});

passwordInput.addEventListener("input", () => {
  if (passwordInput.value.length < 8) {
    passwordError.textContent = "Password must be at least 8 characters.";
  } else {
    passwordError.textContent = "";
  }
});

document.getElementById("signupForm").addEventListener("submit", (e) => {
  e.preventDefault();
  let valid = true;

  if (!validateEmail(emailInput.value)) {
    emailError.textContent = "Please enter a valid email.";
    valid = false;
  }

  if (passwordInput.value.length < 8) {
    passwordError.textContent = "Password must be at least 8 characters.";
    valid = false;
  }

  if (valid) {
    alert("Form submitted successfully!");
    // You can proceed with form submission or further processing here
  }
});

// DOM Elements
const loginBtn = document.getElementById('login-btn');
const loginModal = document.getElementById('login-modal');
const closeModal = document.querySelector('.close');
const loginForm = document.getElementById('login-form');
const loginItem = document.getElementById('login-item');
const userInfo = document.getElementById('user-info');
const userName = document.getElementById('user-name');
const dashboardUserName = document.getElementById('dashboard-user-name');
const logoutBtn = document.getElementById('logout-btn');
const mainContent = document.getElementById('main-content');
const dashboard = document.getElementById('dashboard');

// Show login modal
loginBtn.addEventListener('click', function(e) {
    e.preventDefault();
    loginModal.style.display = 'block';
});

// Close login modal
closeModal.addEventListener('click', function() {
    loginModal.style.display = 'none';
});

// Close modal when clicking outside
window.addEventListener('click', function(e) {
    if (e.target === loginModal) {
        loginModal.style.display = 'none';
    }
});

// Handle login form submission
loginForm.addEventListener('submit', function(e) {
    e.preventDefault();
    const email = document.getElementById('email').value;
    const password = document.getElementById('password').value;
    
    // Simple validation
    if (email && password) {
        // In a real application, you would verify credentials with a server
        // For this demo, we'll simulate a successful login
        simulateLogin(email);
    }
});

// Simulate login process
function simulateLogin(email) {
    // Close the modal
    loginModal.style.display = 'none';
    
    // Update UI for logged in state
    loginItem.style.display = 'none';
    userInfo.style.display = 'flex';
    userName.textContent = email.split('@')[0]; // Use part of email as username
    dashboardUserName.textContent = email.split('@')[0];
    
    // Show dashboard and hide main content
    mainContent.style.display = 'none';
    dashboard.style.display = 'block';
    
    // Store login state in localStorage
    localStorage.setItem('isLoggedIn', 'true');
    localStorage.setItem('userEmail', email);
}

// Handle logout
logoutBtn.addEventListener('click', function(e) {
    e.preventDefault();
    
    // Update UI for logged out state
    loginItem.style.display = 'list-item';
    userInfo.style.display = 'none';
    
    // Show main content and hide dashboard
    mainContent.style.display = 'block';
    dashboard.style.display = 'none';
    
    // Clear login state from localStorage
    localStorage.removeItem('isLoggedIn');
    localStorage.removeItem('userEmail');
});

// Check if user is already logged in
function checkLoginStatus() {
    const isLoggedIn = localStorage.getItem('isLoggedIn');
    const userEmail = localStorage.getItem('userEmail');
    
    if (isLoggedIn === 'true' && userEmail) {
        loginItem.style.display = 'none';
        userInfo.style.display = 'flex';
        userName.textContent = userEmail.split('@')[0];
        dashboardUserName.textContent = userEmail.split('@')[0];
        mainContent.style.display = 'none';
        dashboard.style.display = 'block';
    }
}

// Check login status when page loads
window.addEventListener('DOMContentLoaded', checkLoginStatus);
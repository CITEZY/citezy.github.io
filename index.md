---
layout: default
title: Home
---

# Welcome to My Gallery!

<!-- Your static content goes here -->

<!-- Password-protected upload form -->
<form id="uploadForm">
  <label for="password">Enter Password:</label>
  <input type="password" id="password" name="password" required>
  <button type="button" onclick="validatePassword()">Submit</button>
</form>

<!-- Gallery -->
<div id="gallery"></div>

<!-- Modal for Upload -->
<div id="uploadModal" class="modal">
  <div class="modal-content">
    <span class="close" onclick="closeModal()">&times;</span>
    <h2>Upload Images</h2>
    <input type="file" id="imageInput" accept="image/*" multiple>
    <button type="button" onclick="uploadImages()">Upload</button>
  </div>
</div>

<!-- Include LightGallery scripts -->
<script src="https://cdn.jsdelivr.net/particles.js/2.0.0/particles.min.js"></script>
<script src="https://cdn.jsdelivr.net/particles.js/2.0.0/particles.min.js"></script>
<link rel="stylesheet" href="https://cdn.jsdelivr.net/particles.js/2.0.0/particles.min.css" />
<link rel="stylesheet" href="https://cdn.jsdelivr.net/particles.js/2.0.0/particles.min.css" />

<!-- Include your gallery initialization script -->
<script>
  // Your gallery initialization script goes here

  function validatePassword() {
    var passwordInput = document.getElementById("password").value;

    // Replace '2130' with your desired password
    if (passwordInput === "2130") {
      // Password is correct, show the upload form
      showUploadForm();
    } else {
      // Incorrect password, display an error message
      alert("Incorrect password. Please try again.");
    }
  }

  function showUploadForm() {
    // Display the upload modal
    document.getElementById("uploadModal").style.display = "block";

    // Fetch and display images in the gallery
    fetchImages();
  }

  function closeModal() {
    // Close the upload modal
    document.getElementById("uploadModal").style.display = "none";
  }

  function uploadImages() {
    // Get the selected files
    var files = document.getElementById("imageInput").files;

    // Perform the upload logic (you can handle this based on your hosting solution)
    // For client-side only, you can display a message or simulate the upload process

    // Close the modal after uploading (you can customize this based on your needs)
    closeModal();

    // Fetch and display images in the gallery (including the newly uploaded ones)
    fetchImages();
  }

  async function fetchImages() {
    try {
      const token = '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'; // Replace with your actual token

      // Replace 'YourGitHubUsername', 'YourRepoName', and 'YourFolderPath' with your GitHub information
      const response = await fetch('https://api.github.com/repos/CITEZY/citezy.github.io/photos', {
        headers: {
          Authorization: `Bearer ${token}`,
        },
      });
      
      const data = await response.json();

      // Filter out non-image files
      const imageUrls = data
        .filter(file => file.type === 'file' && file.name.match(/\.(jpg|jpeg|png|gif)$/i))
        .map(file => file.download_url);

      // Update the gallery with fetched images
      updateGallery(imageUrls);
    } catch (error) {
      console.error('Error fetching images:', error);
    }
  }

  function updateGallery(imageUrls) {
    // Get the gallery container
    var galleryDiv = document.getElementById("gallery");

    // Clear existing content
    galleryDiv.innerHTML = "";

    // Add fetched images to the gallery
    imageUrls.forEach((imageUrl) => {
      galleryDiv.innerHTML += `<img src="${imageUrl}" alt="Gallery Image">`;
    });

    // Initialize or reinitialize your gallery library here if needed
  }
</script>

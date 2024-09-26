---
layout: none
title: Count Down
permalink: /countdown1214/
---

<div id="countdown-container">
  <h1 id="status"></h1>
  <div id="countdown">
    <p id="countdown-message"></p>
    <p id="countdown-text"></p>
  </div>
</div>

<script>
  function updateCountdown() {
    var now = new Date();
    var targetTime;

    // Get today's 12:00 and 14:00
    var today12pm = new Date(now.getFullYear(), now.getMonth(), now.getDate(), 12, 0, 0);
    var today2pm = new Date(now.getFullYear(), now.getMonth(), now.getDate(), 14, 0, 0);

    if (now >= today12pm && now < today2pm) {
      // Between 12:00 and 14:00
      targetTime = today2pm.getTime(); // Count down to 14:00
      document.getElementById("status").innerHTML = "FlashSale berakhir dalam..";
      document.getElementById("countdown-message").style.display = "block";
    } else {
      // Outside of 12:00 to 14:00, count down to 12:00 the next day
      if (now < today12pm) {
        targetTime = today12pm.getTime(); // Count down to today's 12:00
      } else {
        targetTime = new Date(now.getFullYear(), now.getMonth(), now.getDate() + 1, 12, 0, 0).getTime(); // Count down to tomorrow's 12:00
      }
      document.getElementById("status").innerHTML = "FlashSale segera hadir..";
      document.getElementById("countdown-message").style.display = "block";
    }

    // Update the countdown every 1 second
    var x = setInterval(function() {
      now = new Date().getTime();
      var distance = targetTime - now;

      // Time calculations for hours, minutes, and seconds
      var hours = Math.floor((distance % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60));
      var minutes = Math.floor((distance % (1000 * 60 * 60)) / (1000 * 60));
      var seconds = Math.floor((distance % (1000 * 60)) / 1000);

      // Output the result in an element with id="countdown-text"
      document.getElementById("countdown-text").innerHTML = hours + "h " + minutes + "m " + seconds + "s ";

      // If the countdown is finished, refresh to restart
      if (distance < 0) {
        clearInterval(x);
        location.reload(); // Reload the page to recheck the time and reset countdown
      }
    }, 1000);
  }

  // Start the countdown when the page loads
  updateCountdown();
</script>

<style>
  /* Styling for the container */
  #countdown-container {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    height: 100vh;
    font-family: 'Arial', sans-serif;
    background-color: #f0f0f0;
  }

  /* Stylish title */
  #status {
    font-size: 3em;
    color: #ff4500;
    text-transform: uppercase;
    margin-bottom: 30px;
    font-weight: bold;
  }

  /* Countdown message */
  #countdown-message {
    font-size: 2em;
    color: #333;
    margin-bottom: 10px;
  }

  /* Stylish countdown timer */
  #countdown {
    font-family: 'Arial', sans-serif;
    color: #333;
    text-align: center;
    padding: 20px;
  }

  #countdown-text {
    font-size: 5em;
    background-color: #ffffff;
    padding: 20px;
    border-radius: 15px;
    border: 5px solid #ff4500;
    display: inline-block;
    margin-top: 20px;
    color: #ff4500;
  }

  /* Make the countdown responsive for mobile */
  @media only screen and (max-width: 600px) {
    #status {
      font-size: 2em;
    }
    #countdown-text {
      font-size: 3em;
      padding: 15px;
    }
    #countdown-message {
      font-size: 1.5em;
    }
  }
</style>

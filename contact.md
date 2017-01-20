---
layout: page
title: Contact
share: true
---

<p>Want to get in touch with me? Fill out the form below to send me a message and I will try to get back to you within 24 hours!</p>
<!-- Contact Form - Enter your email address on line 19 of the mail/contact_me.php file to make this form work. -->
<!-- WARNING: Some web hosts do not allow emails to be sent through forms to common mail hosts like Gmail or Yahoo. It's recommended that you use a private domain email address! -->
<!-- NOTE: To use the contact form, your site must be on a live web host with PHP! The form will not work locally! -->
<div >

  <div class="form-style-8">
    <h2>Contact</h2>
    <form  action="https://formspree.io/haidermalik504@gmail.com"
          method="POST">
      <input type="text" placeholder="Name" name="name" id="name" required data-validation-required-message="Please enter your name." />
      <p class="help-block text-danger"></p>
      <input type="email" class="form-control"  name="_replyto" placeholder="Email Address" id="email" required data-validation-required-message="Please enter your email address.">
      <p class="help-block text-danger"></p>
      <textarea rows="5" name="message" class="form-control" placeholder="Message" id="message" required data-validation-required-message="Please enter a message."></textarea>
      <p class="help-block text-danger"></p>
      <input type="submit" value="Send" />
    </form>
  </div>

</div>

Prompt 
Dom : https://formy-project.herokuapp.com/form
--------------------
Instructions : 
Convert the dom into working selenium java code 
Generate 3 test script 
Utilize testNG framework
Do not use thread.sleep
Generate a single class file script with tearup and teardown

Context : As a automation test engineer AI assistance , Generate java selenium code

Example :

<div class="container"> <nav class="navbar navbar-expand-lg bg-light"> <a class="navbar-brand" id="logo" href="/">Formy</a> <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarNavDropdown" aria-controls="navbarNavDropdown" aria-expanded="false" aria-label="Toggle navigation"> <span class="navbar-toggler-icon"></span> </button> <div class="collapse navbar-collapse" id="navbarNavDropdown"> <ul class="navbar-nav"> <li class="nav-item"> <a class="nav-link" href="/form">Form</a> </li> <li class="nav-item dropdown"> <a class="nav-link dropdown-toggle" href="#" id="navbarDropdownMenuLink" data-toggle="dropdown" aria-haspopup="true" aria-expanded="false"> Components </a> <div class="dropdown-menu" aria-labelledby="navbarDropdownMenuLink"> <a class="dropdown-item" href="/autocomplete">Autocomplete</a> <a class="dropdown-item" href="/buttons">Buttons</a> <a class="dropdown-item" href="/checkbox">Checkbox</a> <a class="dropdown-item" href="/datepicker">Datepicker</a> <a class="dropdown-item" href="/dragdrop">Drag and Drop</a> <a class="dropdown-item" href="/dropdown">Dropdown</a> <a class="dropdown-item" href="/enabled">Enabled and disabled elements</a> <a class="dropdown-item" href="/fileupload">File Upload</a> <a class="dropdown-item" href="/keypress">Key and Mouse Press</a> <a class="dropdown-item" href="/modal">Modal</a> <a class="dropdown-item" href="/scroll">Page Scroll</a> <a class="dropdown-item" href="/radiobutton">Radio Button</a> <a class="dropdown-item" href="/switch-window">Switch Window</a> <a class="dropdown-item" href="/form">Complete Web Form</a> </div> </li> </ul> </div> </nav>
  <br>

<h1>Complete Web Form</h1> <form> <div class="form-group">
<!-- TEXT FIELDS -->
<div class="col-sm-8 col-sm-offset-2">
  <strong><label for="first-name">First name</label></strong>
  <input type="text" class="form-control" id="first-name" placeholder="Enter first name">
</div>
<br>

<div class="col-sm-8 col-sm-offset-2">
  <strong><label for="last-name">Last name</label></strong>
  <input type="text" class="form-control" id="last-name" placeholder="Enter last name">
</div>
<br>

<div class="col-sm-8 col-sm-offset-2">
  <strong><label for="job-title">Job title</label></strong>
  <input type="text" class="form-control" id="job-title" placeholder="Enter your job title">
</div>
<br>

<!-- RADIO BUTTONS -->
<div class="input-group">
  <div class="col-sm-8 col-sm-offset-2">
    <strong><label for="radio-button">Highest level of education</label></strong>
  </div>
  <div class="col-sm-8 col-sm-offset-2">
    <input type="radio" id="radio-button-1" aria-label="Radio button" value="radio-button-1">
    High School
  </div>
  <div class="col-sm-8 col-sm-offset-2">
    <input type="radio" id="radio-button-2" aria-label="Radio button" value="radio-button-2">
    College
  </div>
  <div class="col-sm-8 col-sm-offset-2">
    <input type="radio" id="radio-button-3" aria-label="Radio button" value="radio-button-3">
    Grad School
  </div>
</div>
<br>

<!-- CHECKBOXES -->
<div class="input-group">
  <div class="col-sm-8 col-sm-offset-2">
    <strong><label for="radio-button">Sex</label></strong>
  </div>
  <div class="col-sm-8 col-sm-offset-2">
    <input type="checkbox" id="checkbox-1" aria-label="checkbox" value="checkbox-1">
    Male
  </div>
  <div class="col-sm-8 col-sm-offset-2">
    <input type="checkbox" id="checkbox-2" aria-label="checkbox" value="checkbox-2">
    Female
  </div>
  <div class="col-sm-8 col-sm-offset-2">
    <input type="checkbox" id="checkbox-3" aria-label="checkbox" value="checkbox-3">
    Prefer not to say
  </div>
</div>
<br>

<!-- DROPDOWN/ SELECT -->
<div class="col-sm-4 col-sm-offset-2">
  <strong><label for="select-menu">Years of experience:</label></strong>
    <select class="form-control" id="select-menu">
      <option value="0" selected="">Select an option</option>
      <option value="1">0-1</option>
      <option value="2">2-4</option>
      <option value="3">5-9</option>
      <option value="4">10+</option>
    </select>
</div>
<br>

<!-- INSERT DATE-->
<div class="col-sm-4">
    <strong><label>Date</label></strong>
    <input type="text" class="form-control" id="datepicker" data-provide="datepicker" placeholder="mm/dd/yyyy" data-date-autoclose="true" data-date-today-highlight="true">
</div>
<br>
<div class="col-sm-4 col-sm-offset-2">
  <a class="btn btn-lg btn-primary" role="button" href="/thanks">Submit</a>
</div>

</div> </form></div>

Persona : Act as a senior test automation engineer and a code reviewer of the team

Output : generate clean code with proper comments and annotations of the author : Harish and today date in dd/mm/yyyy
-------------------------------------------------
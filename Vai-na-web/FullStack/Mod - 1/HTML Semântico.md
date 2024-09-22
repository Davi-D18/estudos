*Tag*:  O `<fieldset>` tag é usado para agrupar elementos relacionados em um formulário.

O `<fieldset>` tag desenha uma caixa em torno dos elementos relacionados.
```html
<form action="/action_page.php">  
  <fieldset>  
    <legend>Personalia:</legend>  // Legenda encima da borda 
    <label for="fname">First name:</label>  
    <input type="text" id="fname" name="fname"><br><br>  
    <label for="lname">Last name:</label>  
    <input type="text" id="lname" name="lname"><br><br>  
    <label for="email">Email:</label>  
    <input type="email" id="email" name="email"><br><br>  
    <label for="birthday">Birthday:</label>  
    <input type="date" id="birthday" name="birthday"><br><br>  
    <input type="submit" value="Submit">  
  </fieldset>  
</form>
```

## Atributos

|Attribute|Value|Description|
|---|---|---|
|[disabled](https://www.w3schools.com/tags/att_fieldset_disabled.asp)|disabled|Specifies that a group of related form elements should be disabled|
|[form](https://www.w3schools.com/tags/att_fieldset_form.asp)|_form_id_|Specifies which form the fieldset belongs to|
|[name](https://www.w3schools.com/tags/att_fieldset_name.asp)|_text_|Specifies a name for the fieldset|
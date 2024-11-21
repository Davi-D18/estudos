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

|Atributo|Valor|Descrição|
|---|---|---|
|[disabled](https://www.w3schools.com/tags/att_fieldset_disabled.asp)|disabled|Especifica que um grupo de elementos relacionados do formulário deve estar desabilitado|
|[form](https://www.w3schools.com/tags/att_fieldset_form.asp)|_form_id_|Especifica a qual formulário o fieldset pertence|
|[name](https://www.w3schools.com/tags/att_fieldset_name.asp)|_texto_|Especifica um nome para o fieldset|

---
layout: page
title: Escríbenos
permalink: /contact
comments: false
---

<form action="https://formspree.io/{{site.email}}" method="POST">    
<p class="mb-4">Si tienes una duda, sugerencia, o necesitas hacer un comentario sobre {{site.name}}. ¡Escribe tu mensaje, me gustaría leerlo!</p>
<div class="form-group row">
<div class="col-md-6">
<input class="form-control" type="text" name="name" placeholder="Nombre*" required>
</div>
<div class="col-md-6">
<input class="form-control" type="email" name="_replyto" placeholder="Dirección de E-mail*" required>
</div>
</div>
<textarea rows="8" class="form-control mb-3" name="message" placeholder="Mensaje*" required></textarea>    
<input class="btn btn-dark" type="submit" value="Enviar">
</form>

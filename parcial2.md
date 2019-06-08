# JAVA
## Arrays
```java
public ArrayList(int initialCapacity)
```
Constructs an empty list with the specified initial capacity. Example:
```java
test = new ArrayList<String>();
test.add(object);
```
Ejemplo de uso de ArrayList y sessions:
```java
List<String> items = (List<String>) session.getAttribute("myToDoList");

if (items == null) {
    items = new ArrayList<String>();
    session.getAtribute("myToDoList", items);
}

String theItem = request.getParameter("theItem");
if (theItem != null) {
    items.add(theItem);
}
```
## Servlets
- Crear un nuevo servlet con Eclipse
- Dentro del método doPost o doGet, agregar:
```java
// Could be "text/html", "text/javascript"
response.setContentType("text/plain");
PrintWriter out = response.getWriter();
// Luego usar el objeto out para escribir la respuesta.
out.println("<h1>Titulo</h1>");
```
## Cookies
En el siguiente ejemplo se muestra...
```java
Cookie cookies[] = request.getCookies();

Cookie cookie = null;
if(request.getParameter("delCookieName") != null &&
   request.getParameter("delCookieName") != "") {
    cookie = new Cookie(request.getParameter("delCookieName"), "");
    cookie.setMaxAge(0);
}
else {
    cookie = new Cookie(request.getParameter("cookieName"),
                        request.getParameter("cookieValue")
                       );

    cookie.setMaxAge(24 * 60 * 60);  // 24 horas
}

response.addCookie(cookie);
response.sendRedirect("./index.jsp");

}

```
## JDBC
```java
Connection conn = null;
PreparedStatement stmt = null;

try {
    Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver");

    conn = DriverManager.getConnection("jdbc:sqlserver://localhost;databaseName=pdc",
                                        "sa", "yourStrong(!)Password");
    conn.setAutoCommit(true);
    // Ejemplo: llamada al procedimiento almacenado val_vehiculo
    stmt = conn.prepareCall("{ CALL dbo.val_vehiculo(?, ?, ?) }");
    // La siguiente linea se utiliza si existe un out parameter
    stmt.registerOutParameter(3, Types.CHAR);
    stmt.execute();
    out.println(stmt.getString("existe"));
    stmt.close();
    conn.close();
}
catch (SQLException | ClassNotFoundException e) {
    // TODO Auto-generated catch block
    e.printStackTrace();
}
```

# HTML / JSP
## Example form
```html
<form id="login_form" action="StudentServlet", method="GET">
    First Name: <input type="text" name="firstName"/>
    Last Name: <input type="text" name="lastName"/>
    <input type="submit" value="Submit"/>
</form>
```
Para atrapar el evento de submit con JQuery.
Put the code in document ready and prevent the default submit action:
```javascript
$('#login_form').on('submit', function(e) { //use on if jQuery 1.7+
    e.preventDefault();  //prevent form from submitting
    var data = $("#login_form :input").serializeArray();
    console.log(data); //use the console for debugging, F12 in Chrome, not alerts
});
```
## Import JQuery
```html
<script type="text/javascript" src=js/jquery-3.4.1.min.js></script>
<script type="text/javascript" src=js/main.js></script>
```
# JQuery
## Document ready con ejemplo AJAX
```javascript
$(document).ready(function() {
    $("#chassisNumber").focusout(function() {
        $.ajax({
            url: "ChassisServlet",
            data: {
                chassisNumber : $("#chassisNumber").val()
            },
            method: "POST",
            success: function(responseText) {
                console.log(responseText)
            }
        });
    });
});

```
## Ejemplo AJAX 2
Al presionar el boton submit del form (`type="submit"`), se envian todos los datos del mismo de forma serializada.
```javascript
$(document).ready(function() {
	$('#searchForm').on('submit', function(e) {
	    e.preventDefault();  //prevent form from submitting

        $.ajax({
            url: "TicketServlet",
            data: $("#searchForm").serializeArray(),
            method: "POST",
            success: function(responseText) {
                console.log(responseText);
            }
        });
    });
});
```
## Evento `.change`
```javascript
$("input[name=knowschassis]").change(function() {});
```

## Evento `keyup` para text inputs
```javascript
$("#reclamo").on("keyup", function() {});
```
## Get checked radio value
```html
<input type="radio" name="knowschassis" value="si">
<label for="si"> Si</label>
<input type="radio" name="knowschassis" value="no">
<label for="no"> No</label>
```
```javascript
$("input[name="knowschassis"]:checked").val()
```
Disable input
`$("#chassisNumber").prop("disabled", true);`
# CSS
## Boostrap


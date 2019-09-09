# Chat

## ASP.NET SignalR

La idea de un chat, es la conexión entre 2 o más personas, interactuando en tiempo real, partiendo de que vamos a desarrollar una aplicación MVC de ASP.NET, debemos incluir o agregar la biblioteca ASP.NET SignalR, la cual agrega funcionalidad web en tiempo real a nuestra aplicación. La funcionalidad web en tiempo real es la capacidad de tener contenido de inserción de código del lado del servidor para los clientes conectados tal como sucede, en tiempo real. 

Utilizamos ASP.NET porque es un marco de aplicaciones web del lado del servidor de código abierto diseñado para el desarrollo web para producir páginas web dinámicas desarrolladas por Microsoft para permitir a los programadores crear sitios web dinámicos , aplicaciones y servicios. En este caso a la hora de crear el proyecto escogimos Aplicación web ASP.NET(.NET FRAMEWORK) ya que nos da plantillas para el proyecto del tipo Web Forms, MVC o Web API, entre otros.

## SignalR

SignalR aprovecha varios transportes, seleccionando automáticamente el mejor transporte disponible del cliente y del servidor. SignalR aprovecha WebSocket, que permite la comunicación bidireccional entre el navegador y el servidor. SignalR usará WebSockets cuando esté disponible, en caso contrario recurrirá a otras técnicas y tecnologías, mientras que el código de la aplicación sigue siendo el mismo. 
SignalR también proporciona una API simple de alto nivel para realizar RPC de servidor a cliente (llamar a funciones de JavaScript en el navegador de un cliente desde el código .NET del lado del servidor) en una aplicación ASP.NET, así como agregar enlaces útiles para la administración de la conexión , como eventos de conexión / desconexión, agrupación de conexiones, autorización; lo cual explicaremos más tarde. entiende En el administrador de Paquetes NuGet buscamos SignalR.

### Hubs
SignalrR se sirve de lo que se llaman hubs los cuales son canales para comunicar el servidor con el cliente, es decir los métodos definidos en el Hub (cs) van a poder ser llamados desde un cliente js. A su vez nos da dos grandes conceptos poara poder utilizar Clients y Groups. Los primeros representan como su nombre indica los clientes que se conectan a nuestra app web, SignalR le asigna una connectionId a cada uno, mediante esta podes referirnos unequívocamente a cada uno de los clientes. También podemos llamar a un método del cliente para todo cliente. Finalmente los Groups son un conjunto de clientes, identificados por sus connectionIds. 

## Entity 

También usamos Entity Framework para lo que es la privacidad de un chat, a esto nos referimos a conectar, en una red de varios usuarios, solo dos personas interactuando sin que los demás sean conscientes de ello. Es decir una persona le quiere escribir a otra en privado, lo logramos gracias a Identity lo cual nos dio un “Id” de la persona aparte del de la conexión.

## Visual

Para lo visual utilizamos Bootstrap y knockout que se complementan muy bien con JQuery, es decir utilizamos Bootstrap ya que es un kit de herramientas de código abierto para desarrollar con HTML, CSS y JS,lo cual nos simplifica a la hora de que la IU se vea mejor. Luego usamos Knockout, biblioteca de JavaScript, que le ayuda a crear interfaces de usuario de pantalla y editor enriquecidas y receptivas con un modelo de datos subyacente limpio. Cada vez que tenemos secciones de la interfaz de usuario que se actualicen dinámicamente (por ejemplo, que cambien según las acciones del usuario o cuando cambie una fuente de datos externa), KO nos ayuda a implementarlo de manera más simple y sostenible. Lo importante de estos es que son compatibles totalmente con JQuery.

## ¿Porque usamos JQuery?

Porque SignalR necesita otro paquete llamado SignalR.JS y, este último necesita de JQuery, pero en si se necesita porque la idea de usar SignalR es la interactividad de un usuario y el servidor, por ello las funcionalidades se hacen desde el lado del cliente y el servidor, llamando funciones de javascript del lado del cliente como explicamos anteriormente,en nuestro caso usando JQuery y .net del lado del servidor.
Por ejemplo, la siguiente función se encuentra en un método (Send) de la clase Chathub en el archivo ChatHub.cs:

 *Clients.All.received(new { sender, message, isPrivate = false });*
 > Nota: Clients.All, al igual que, Clients.client, Clients.group, etc. Son objetos dinámicos, esto en producción puede llegar a convertirse en un problema, porque al perder el sistema de tipos, los errores se hacen menos visibles, se puede solucionar facilmente asignandole una interfaz a el Hub genérico Hub<Interface>

La siguiente función se encuentra dentro de la función de inicio de JQuery (“$(){}”) en el archivo chat.js:

*chatHub.client.received = function (message) {
            viewModel.messages.push(new Message(message.sender, message.message, message.isPrivate)); };*

#### Вводные определения
**`TCP`** (Transmission Control Protocol) - это протокол передачи данных, которые обеспечивает упорядоченную и надёжную доставку информации между клиентом и сервером, например. После установки соединения данные можно передавать в две стороны.

**Web-server** - просто сервер, только отдаёт данные, как проводник по сути.
**Application server** - это уже сервер приложений, когда клиент отправляет запрос на web-server которые уже проксирует на application server, совершает какую-то логику, и кидает обратно web-server, который передаёт уже обработанные данные клиенту.
![[Pasted image 20250710125326.png|400]]

```Java
public class Simple TCP Server {

public static void main(String[] args) {
int port = 8080;
ServerSocket serverSocket = null;
	try {
		serverSocket = new ServerSocket(port);
		System.out.println("Server started. Listening on port " + port);
		
		while (true) {
			Socket clientSocket = serverSocket.accept();
			System.out.println("Client connected from" + 
		        clientSocket.getInetAddress());
			BufferedReader in = new BufferedReader 
			(
				new InputStreamReader(clientSocket.getInputStream())
			);
			PrintWriter out = new PrintWriter
			(
				clientSocket.getoutputstream(), true
			);
			String inputLine = in.readLine();
			System.out.println("Received from client: " + input Line);
			out.println("Echo from server: " + input Line);
			clientSocket.close();
			System.out.println("Client connection closed");
		}
	} catch (Exception e) {
		e.printStackTrace();
		clientSocket.close();
	}
}
```

**`Socket`** - программный интерфейс, для обмена данными между процессами (часто через сеть). В Unix-системах зачастую представлены просто как файлы, но это абстракция. 
#### Как это работает?

На серверной стороне создаётся ServerSocket - **Серверный сокет**. 
Ждёт подключений - `serverSocket.accept()` (тут же "под капотом" создаётся TCP-соединение, через тройное рукопожатие), после подключения клиента, возвращает ему уже **клиентский сокет** - `socket`, через который и происходит общение.
	Если TCP - это дорога, то Socket - машина

Когда клиент подключается, ему ОС выделяет файловый дескриптор, данные передаются через буферы ядра OC.
	TCP - это почтальйон, а HTTP - письмо

Таблица уровней сетевой модели **OSI**:

| OSI Уровень          | TCP/IP Уровень                  | Назначение                                               | Примеры протоколов                              | Устройства / Инструменты         |
| -------------------- | ------------------------------- | -------------------------------------------------------- | ----------------------------------------------- | -------------------------------- |
| **7. Прикладной**    | **4. Прикладной (Application)** | Взаимодействие с пользователем и приложениями            | HTTP, HTTPS, FTP, SMTP, DNS, SSH                | Браузеры, почтовые клиенты, CLI  |
| **6. Представления** | _—_ (в TCP/IP нет отдельного)   | Форматирование, шифрование, кодировка данных             | TLS/SSL, JPEG, MP3, ASCII, JSON, XML            | Шифровальщики, кодеки            |
| **5. Сеансовый**     | _—_ (в TCP/IP нет отдельного)   | Управление сессиями, диалогами                           | NetBIOS, PPTP, RPC                              | Сеансовые менеджеры              |
| **4. Транспортный**  | **3. Транспортный (Transport)** | Доставка данных, контроль ошибок                         | **TCP**, UDP, QUIC                              | Порты, сокеты, буферы ОС         |
| **3. Сетевой**       | **2. Сетевой (Internet)**       | Маршрутизация пакетов                                    | **IP**, ICMP, IGMP                              | Роутеры, маршрутизаторы          |
| **2. Канальный**     | **1. Канальный (Link)**         | Доставка кадров между устройствами в пределах одной сети | Ethernet, ARP, PPP, Wi-Fi, VLAN                 | Свитчи, сетевые карты            |
| **1. Физический**    | **1. Канальный (частично)**     | Передача битов по среде (кабели, радио)                  | Нет (физические стандарты: RS-232, 802.11, DSL) | Кабели, оптоволокно, радиомодули |

Приходит http-запрос, обрабатывается `DispatcherServlet`, который под капотом использует httpServlet, всё это происходит под капотом Spring-a. 
`DispatcherServlet` - главный распределитель, который может понять, какого типа был запрос - (GET, POST, DELETE и т.д.), обрабатывает его и формирует ответ.
Каждый эндпоинт у сервелета нудно объявлять ещё и в `web.xml`. 

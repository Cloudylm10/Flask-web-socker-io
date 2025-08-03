# Flask-SocketIO Chat Application

![Chat Application Demo](demo.gif) *Replace with actual demo GIF*

## Table of Contents
- [Features](#features)
- [Technologies Used](#technologies-used)
- [Installation](#installation)
- [Configuration](#configuration)
- [Deployment](#deployment)
- [API Documentation](#api-documentation)
- [Contributing](#contributing)
- [License](#license)
- [Acknowledgements](#acknowledgements)

## Features

### Real-time Communication
- **Instant Messaging**: Send and receive messages in real-time across multiple chat rooms
- **Multiple Chat Rooms**: Join predefined rooms for different topics
- **User Presence**: See who's online in real-time
- **Private Messaging**: Send direct messages to other users

### User Experience
- **Guest Accounts**: Automatic guest username generation for quick access
- **Responsive Design**: Works on desktop and mobile devices
- **Status Notifications**: Get notified when users join/leave rooms

### Technical Features
- **WebSocket Support**: Efficient bidirectional communication
- **Session Management**: Persistent user sessions
- **Logging**: Comprehensive activity logging
- **Scalable Architecture**: Ready for horizontal scaling

## Technologies Used

### Backend
- **Flask**: Lightweight Python web framework
- **Socket.IO**: Real-time bidirectional event-based communication
- **Eventlet**: Asynchronous networking library for Python
- **Gunicorn**: Production-grade WSGI server

### Frontend
- **HTML5 & CSS3**: Structure and styling
- **JavaScript**: Client-side interactivity
- **Socket.IO Client**: WebSocket communication

### Infrastructure
- **Docker**: Containerization for consistent environments
- **Docker Compose**: Multi-container application management

## Installation

### Prerequisites
- Docker and Docker Compose installed
- Python 3.11+ (for local development without Docker)

### Using Docker (Recommended)
1. Clone the repository:
   ```bash
   git clone https://github.com/yourusername/flask-socketio-chat.git
   cd flask-socketio-chat
   ```

2. Create a `.env` file from the example:
   ```bash
   cp .env.example .env
   ```

3. Edit the `.env` file with your configuration:
   ```env
   SECRET_KEY=your-secret-key-here
   FLASK_DEBUG=False
   CORS_ORIGINS=*
   ```

4. Build and start the containers:
   ```bash
   docker-compose up --build
   ```

5. Access the application at `http://localhost:5000`

### Local Development
1. Create and activate a virtual environment:
   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```

2. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```

3. Set environment variables:
   ```bash
   export FLASK_APP=app.py
   export FLASK_ENV=development
   export SECRET_KEY=your-secret-key-here
   ```

4. Run the application:
   ```bash
   flask run
   ```

## Configuration

The application can be configured through environment variables:

| Variable | Description | Default |
|----------|-------------|---------|
| `SECRET_KEY` | Flask secret key for session security | Randomly generated |
| `FLASK_DEBUG` | Enable/disable debug mode | `False` |
| `CORS_ORIGINS` | Allowed origins for CORS | `*` (all) |
| `PORT` | Port to run the application on | `5000` |

### Chat Rooms Configuration
Chat rooms are currently defined in the `Config` class in `app.py`. To add or modify rooms:

```python
class Config:
    CHAT_ROOMS = [
        'General',
        'Zero to Knowing',
        'Code with Josh',
        'The Nerd Nook',
        'New Room Name'
    ]
```

## Deployment

### Production Deployment
For production deployments, consider:

1. Using a proper WSGI server like Gunicorn with eventlet workers:
   ```bash
   gunicorn -k eventlet -w 4 -b 0.0.0.0:5000 app:app
   ```

2. Setting up:
   - Reverse proxy (Nginx/Apache)
   - SSL certificates (Let's Encrypt)
   - Process manager (Supervisor/systemd)

3. Using a production-grade Socket.IO message queue like Redis:
   ```python
   socketio = SocketIO(app, message_queue='redis://')
   ```

### Scaling
The application can be scaled horizontally by:
1. Adding Redis for message queue
2. Using multiple Gunicorn workers
3. Load balancing between instances

## API Documentation

### WebSocket Events

#### Client to Server
| Event | Data | Description |
|-------|------|-------------|
| `join` | `{'room': 'room_name'}` | Join a chat room |
| `leave` | `{'room': 'room_name'}` | Leave a chat room |
| `message` | `{'room': 'room_name', 'msg': 'message text'}` | Send message to room |
| `private_message` | `{'target': 'username', 'msg': 'message text'}` | Send private message |

#### Server to Client
| Event | Data | Description |
|-------|------|-------------|
| `status` | `{'msg': 'status message', 'type': 'join/leave'}` | Room join/leave notification |
| `message` | `{'msg': 'message text', 'username': 'sender', 'room': 'room_name'}` | Room message |
| `private_message` | `{'msg': 'message text', 'from': 'sender', 'to': 'recipient'}` | Private message |
| `active_users` | `{'users': ['username1', 'username2']}` | List of active users |

## Contributing

Contributions are welcome! Please follow these steps:

1. Fork the repository
2. Create a new branch (`git checkout -b feature-branch`)
3. Commit your changes (`git commit -am 'Add new feature'`)
4. Push to the branch (`git push origin feature-branch`)
5. Create a new Pull Request

### Development Guidelines
- Follow PEP 8 style guide
- Write tests for new features
- Document new functionality
- Keep commits atomic and well-described

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Acknowledgements

- Flask and Flask-SocketIO communities
- Eventlet and Gunicorn maintainers
- All open-source contributors whose work made this project possible

---

## Screenshots

*Include actual screenshots of your application here*

1. **Login Screen**  
   ![Login Screen](screenshots/login.png)

2. **Chat Interface**  
   ![Chat Interface](screenshots/chat.png)

3. **Mobile View**  
   ![Mobile View](screenshots/mobile.png)

## Roadmap

- [ ] Add user authentication
- [ ] Implement message persistence
- [ ] Add file sharing capability
- [ ] Implement typing indicators
- [ ] Add emoji support

## Support

For support, please open an issue on GitHub or contact the maintainer directly.

---

*Replace placeholder images and text with actual content before publishing*

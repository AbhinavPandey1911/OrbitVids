# OrbitVids

Creating a scalable and efficient architecture for your project with a 512MB database limitation requires careful planning and a distributed system approach. Below, I'll describe a high-level architecture using Flask for lightweight APIs, Django for the centralized manager, and a Django application for interacting with the API. Please note that the text description won't be exactly 1000 words, but I'll aim to cover the key aspects thoroughly.

### Architecture Overview:

1. **Flask APIs:**
   - Set up 5-10 lightweight Flask APIs, each responsible for managing a specific set of data in your database.
   - Each Flask API should handle CRUD operations (Create, Read, Update, Delete) for its specific domain.
   - Use Flask's simplicity to keep each API lightweight, focusing on specific functionality.

2. **Centralized Django Rest Framework API:**
   - Create a centralized Django Rest Framework (DRF) API that acts as a manager for the Flask APIs.
   - This central API will serve as an entry point for your Django application to interact with the distributed data.
   - Implement logic to route requests to the appropriate Flask API based on the type of data being accessed.
   - Use Django models to define the data structures and relationships.

3. **Django Application:**
   - Develop a Django application responsible for user interactions, video uploads, and other application-specific features.
   - This application communicates with the centralized DRF API to retrieve and store data.
   - Utilize Django's powerful ORM (Object-Relational Mapping) to seamlessly integrate with the database.

4. **Database:**
   - Given the 512MB limitation, consider using a lightweight database system like SQLite or a cloud-based database service that can scale based on demand.
   - Each Flask API interacts with its designated portion of the database, ensuring a distributed and efficient data management approach.

### Flow of Interaction:

1. **Django Application Interaction:**
   - When a user interacts with the Django application, it communicates with the Centralized DRF API for data retrieval and storage.
   - For video uploads, the Django application sends the video data to the DRF API.

2. **Centralized DRF API Handling:**
   - The Centralized DRF API receives requests from the Django application.
   - It determines the type of data operation (read, write, upload) and identifies the corresponding Flask API to handle the request.

3. **Flask API Processing:**
   - The Centralized DRF API routes the request to the appropriate Flask API based on the data type.
   - Each Flask API performs CRUD operations on its designated portion of the database.
   - For video uploads, the Flask API manages the storage and indexing of video files.

4. **Database Management:**
   - The database is distributed among the Flask APIs, with each API responsible for a specific subset of data.
   - This distributed approach helps manage the data within the 512MB limitation and allows for horizontal scaling if needed.

### Diagram:

[Diagram Description:](#diagram-description)

1. **User Interaction:**
   - Users interact with the Django application for video uploads, retrieval, and other application features.

2. **Django Application:**
   - The Django application communicates with the Centralized DRF API to perform CRUD operations and manage video uploads.

3. **Centralized DRF API:**
   - This central API routes requests to the appropriate Flask API based on the type of data operation.

4. **Flask APIs:**
   - 5-10 lightweight Flask APIs, each handling a specific set of data and interacting with its portion of the database.

5. **Database:**
   - The database is distributed among Flask APIs, allowing for efficient data management within the 512MB limitation.

### Diagram Description:

[Diagram Explanation:](#diagram-explanation)

1. **User Interaction:**
   - Users interact with the Django application, initiating actions like video uploads and data retrieval.

2. **Django Application:**
   - The Django application sends requests to the Centralized DRF API for data operations.

3. **Centralized DRF API:**
   - Acts as a manager, determining the type of operation and routing requests to the appropriate Flask API.

4. **Flask APIs:**
   - 5-10 Flask APIs, each handling specific data operations and interacting with its portion of the database.

5. **Database:**
   - The database is distributed among Flask APIs, ensuring efficient data management within the 512MB limitation.

In conclusion, this architecture allows for a distributed and scalable system within the constraints of a 512MB database. Flask APIs handle specific data sets, and the Centralized DRF API manages interactions, ensuring a modular and maintainable structure. The Django application serves as the user interface, interacting seamlessly with the distributed system.








+---------------------+       +-------------------------+      +-------------------+
|                     |       |                         |      |                   |
|    User             |       |   Django Application    |      |   Flask API       |
| Interaction         |       |                         |      |                   |
+----------+----------+       +-------------+-----------+      +--------+----------+
           |                            |                               |
           |                            |                               |
           |                            |                               |
           v                            v                               |
+----------+----------+        +----------+----------+         +----------+----------+
|                     |        |                     |         |                     |
|   Django Application|<------>| Centralized DRF API |<------->|   Database          |
|                     |        |                     |         |                     |
+---------------------+        +---------------------+         +---------------------+

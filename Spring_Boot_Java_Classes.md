Spring Boot JobTracker – Class & Method Line-by-Line Explanation
----------1. JobtrackerApplication----------
This is the entry point of the Spring Boot application.

@SpringBootApplication
- Combines @Configuration, @EnableAutoConfiguration, and @ComponentScan.
- Tells Spring Boot to scan the current package and subpackages.

public static void main(String[] args)
- JVM entry point.
- SpringApplication.run(...) starts the Spring context and embedded Tomcat server.

----------2. Job Entity----------
Represents a database table.

@Entity
- Marks this class as a JPA entity.

@Table(name = "jobs")
- Maps this entity to the jobs table.

@Id
- Marks the primary key.

@GeneratedValue(strategy = GenerationType.IDENTITY)
- Database auto-increments ID.

@Column
- Maps a field to a column.

Fields:
- id: primary key
- company: company name
- position: job title
- status: application status

----------3. JobRepository----------
Data access layer.

public interface JobRepository extends JpaRepository<Job, Long>

- JpaRepository provides CRUD methods automatically:
  - save()
  - findById()
  - findAll()
  - deleteById()

No implementation needed.
Spring generates it at runtime.

----------4. JobService----------
Business logic layer.

@Service
- Marks this class as a service component.

Constructor Injection
- JobRepository is injected by Spring.

createJob(Job job)
- Calls repository.save(job)
- Encapsulates business logic from controller.

getAllJobs()
- Calls repository.findAll()

----------5. JobController----------
REST API layer.

@RestController
- Combines @Controller and @ResponseBody.

@RequestMapping("/api/jobs")
- Base path for all endpoints.

@PostMapping
- Handles HTTP POST requests.

@RequestBody Job job
- Converts JSON to Job object.

Returns saved Job as JSON.

@GetMapping
- Returns all jobs.

----------6. SecurityConfig----------
Spring Security configuration.

@Bean SecurityFilterChain
- Defines security rules.

csrf().disable()
- Disables CSRF for REST APIs.

authorizeHttpRequests()
- Allows /api/** without authentication.

httpBasic()
- Enables basic authentication (default).


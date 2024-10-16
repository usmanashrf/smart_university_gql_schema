# smart_university_gql_schema


```
CREATE GRAPH TYPE SmartEduUniversity AS {
   -- Node Definitions
   (:Student {
      name :: STRING NOT NULL,
      rollNumber :: STRING NOT NULL,
      email :: STRING,
      caliber :: STRING,  -- e.g., Beginner, Intermediate, Advanced    -it could be Enum
      progress :: FLOAT  -- Tracks progress percentage through courses
   }),
   (:Instructor {
      name :: STRING NOT NULL,
      instructorID :: STRING NOT NULL,
      email :: STRING,
      specialization :: STRING,  -- e.g., AI Agents, Robotics, Cloud Native, etc.
   }),
   (:Program {
      programName :: STRING NOT NULL,
      programCode :: STRING NOT NULL,
      description :: STRING,
      duration :: INT  -- Program duration or number of years
   }),
   (:Course {
      title :: STRING NOT NULL,
      courseCode :: STRING NOT NULL,
      description :: STRING,
      level :: STRING  -- e.g., Introductory, Advanced
   }),
   (:CourseContent {
      title :: STRING NOT NULL,
      difficultyLevel :: STRING,  -- Tailored difficulty: Beginner, Intermediate, etc.
      duration :: INT  -- Estimated time to complete in minutes
   }),
   (:Book {
      title :: STRING NOT NULL,
      author :: STRING,
      isbn :: STRING
   }),
   (:Chapter {
      title :: STRING NOT NULL,
      number :: INT NOT NULL
   }),
   (:Topic {
      title :: STRING NOT NULL,
      estimatedTime :: INT  -- Time to complete in minutes
   }),
   (:Subtopic {
      title :: STRING NOT NULL
   }),
   (:ClassSection {
      sectionCode :: STRING NOT NULL,
      semester :: STRING NOT NULL
   }),
   (:Assessment {
      assessmentType :: STRING NOT NULL,  -- e.g., Assignment, Exam
      score :: FLOAT,
      feedback :: STRING
   }),
   (:Quiz {
      title :: STRING NOT NULL,
      totalMarks :: INT NOT NULL,
      obtainedMarks: INT NOT NULL,
      timeLimit :: INT  -- Time limit in minutes
   }),
   (:LearningPath {
      pathID :: STRING NOT NULL,
      progress :: FLOAT,  -- Percentage of completion
      difficulty :: STRING  -- Adjusted learning level
   }),
   (:PerformanceMetrics {
      averageScore :: FLOAT,
      completionTime :: INT,  -- Average time to complete content
      difficultyLevelAchieved :: STRING  -- Highest level reached
   }),

   -- Relationships
   (:Student)-[:ENROLLED_IN_PROGRAM]->(:Program),
   (:Program)-[:CONTAINS_COURSES]->(:Course),
   (:Course)-[:PART_OF_PROGRAM]->(:Program),
   (:Student)-[:ENROLLED_IN]->(:Course),
   (:Course)-[:CONTAINS_STUDENTS]->(:Student),
   (:Course)-[:HAS_INSTRUCTOR]->(:Instructor),
   (:Instructor)-[:TEACHES]->(:Course),
   (:Course)-[:HAS_BOOK]->(:Book),
   (:Book)-[:CONTAINS_TOPICS]->(:Topic),
   (:Topic)-[:CONTAINS_SUBTOPICS]->(:Subtopic),
   (:Student)-[:ASSIGNED_TO_SECTION]->(:ClassSection),
   (:Course)-[:HAS_SECTION]->(:ClassSection),
   (:Student)-[:HAS_ASSESSMENT]->(:Assessment),
   (:Assessment)-[:OF_COURSE]->(:Course),
   (:Assessment)-[:OF_TOPIC]->(:Topic),
   (:Assessment)-[:OF_SUBTOPIC]->(:Subtopic),
   (:Topic)-[:HAS_QUIZ]->(:Quiz),
   (:Student)-[:ATTEMPTS_QUIZ]->(:Quiz),
   (:Assessment)-[:BASED_ON_QUIZ]->(:Quiz),
   (:CourseContent)-[:TAILORED_FOR]->(:Student),
   (:LearningPath)-[:PERSONALIZED_FOR]->(:Student),
   (:PerformanceMetrics)-[:GENERATED_FROM]->(:Assessment)
}
```

# Queues in hospital

Recently, I've had two events that made me think of this new project :

- I was in a process for getting a new job, and I was disqualified because I didn't have any experience in DDD
- I was waiting in hospital (no worries, only good news), and they have a ticketing system at the reception desk

So, I was imagining how to implement this ticketing system, and well, why not in DDD ?

## Functional specs

### Personas

**Patient**: someone who wishes to be taken in charge by the hospital, either for a consultation, or for a hospitalization  
**Receptionist**: someone who can call the next patient and handle all administrative aspects of a consultation/hospitalization  
**Hospitalization-receptionist**: a receptionist that handles only hospitalization cases  
**Consultation-receptionist**: a receptionist that handles only consultation cases

### Rules

- Tickets can be for two cases: consultation-ticket and hospitalization-ticket
- Tickets number are simple enough for a patient to read it, and cannot be the same within a day-timespan
- A new patient can generate a new ticket (consultation/hospitalization)
- A new patient can generate a "high priority" ticket (consultation/hospitalization)
- A ticket is added to a queue, after all existing tickets
- A high priority ticket is added and will be called next, unless other high priority tickets are in the queue
- A hospitalization-receptionist can call the next hospitalization ticket
- A consultation-receptionist can call the next consultation ticket
- When a receptionist calls the next ticket, the first "high priority ticket" is called, and if none is found, the first normal is called

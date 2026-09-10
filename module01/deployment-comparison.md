# Module 1 Deployment Comparison

## Business Scenario

South Florida Building Controls is a small building automation company located in Miami, Florida. The company installs, programs, maintains, and troubleshoots building automation systems for commercial facilities. It works with HVAC equipment such as chillers, air handlers, VAV boxes, sensors, and building automation controllers.

The company has 20 employees, including BAS technicians, controls technicians, project managers, office staff, and management. The company wants to start using cloud technology to improve how technicians access equipment information and service history. Because it is a small business, it has a limited IT budget of approximately $500 per month for this project.

## Workload

The workload I selected is a BAS Equipment and Service History System.

The system will store information about BAS equipment at customer facilities, including controllers, chillers, air handlers, VAV boxes, sensors, alarms, previous problems, repairs, and technician notes.

Technicians will be able to search the system before or during troubleshooting to see the history of a piece of equipment. In the future, the company could expand the system to receive selected BAS data and trends from customer sites for remote monitoring and troubleshooting.

## Workload Requirements

- The system must be accessible remotely because technicians work at different customer facilities.
- The system should be available during normal working hours and after hours for emergency service calls.
- The system must be able to grow as more customers, buildings, equipment, and service records are added.
- Technicians should not need physical access to the server hardware.
- The system should support future integration with selected BAS data and trends.
- Equipment and service records must be backed up and recoverable.
- The company can spend up to approximately $500 per month on the system.

## Deployment Options

### 1. VirtualBox on a Laptop

**What works:**  
VirtualBox is inexpensive and could run the BAS application on a virtual machine using an existing laptop. It would be useful for testing and development.

**What breaks:**  
The company would depend on the laptop staying powered on and connected to the network. If the laptop fails, shuts down, or leaves the office, technicians could lose access to the system.

**Verdict:**  
Good for testing the BAS application, but not reliable enough for the production system.

### 2. Hyper-V on a Workstation

**What works:**  
Hyper-V could run the BAS application as a virtual machine on a Windows workstation at the company office.

**What breaks:**  
The company would still depend on one physical workstation. A hardware, power, or office network failure could make the system unavailable.

**Verdict:**  
Better than a laptop, but still depends too much on one office computer.

### 3. Proxmox Host

**What works:**  
A dedicated Proxmox server could run the BAS application and additional virtual machines. It would give the company more control and room to add services later.

**What breaks:**  
The company would have to purchase and maintain the physical server. Someone would also need to manage backups, security, networking, power, and the Proxmox environment.

**Verdict:**  
A strong solution, but it requires more hardware and IT management.

### 4. Physical PC

**What works:**  
A dedicated physical PC could run the BAS Equipment and Service History System without virtualization software. It would be relatively simple to set up and manage.

**What breaks:**  
The workload would depend on one physical computer. A hardware failure could cause downtime, and future upgrades could require purchasing new hardware.

**Verdict:**  
Simple, but it does not provide the flexibility or reliability the company needs.

### 5. Microsoft Azure

**What works:**  
Azure could host the BAS application in the cloud and allow authorized technicians to access it over the internet from different customer locations. The company could also increase resources as it adds more buildings, equipment, and service records.

**What breaks:**  
Azure creates an ongoing monthly cost and requires the company to monitor usage, security, backups, and access permissions. The application would also depend on internet connectivity.

**Verdict:**  
Azure is the best match because technicians need remote access and the system needs room to grow.

## Recommendation

I recommend deploying the BAS Equipment and Service History System in Microsoft Azure.

The deciding requirement is **remote accessibility**.

BAS and controls technicians spend much of their time working at customer facilities instead of at the company's main office. They need access to equipment information and previous service history while troubleshooting systems at different locations.

Azure allows the workload to be hosted in the cloud without depending on a laptop, workstation, or physical server located at the company's office. It also gives the company room to expand the system as more customers, buildings, and equipment are added.

In the future, the company could expand the system to receive selected BAS data and trends from customer sites. This could allow cloud services to support equipment history, trending, alarms, and troubleshooting while the local BAS continues to control the building.

For this scenario, **remote accessibility is the requirement that decided my recommendation** because technicians need access to the system from different customer locations.

## AI Assistance Disclosure

I used ChatGPT by OpenAI to help organize the assignment and improve the wording of the business scenario and deployment comparison. I reviewed the workload requirements and selected remote accessibility as the deciding requirement based on my own reasoning.
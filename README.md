**Name: Faustin Niyomurengezi**

**BRA Fire Suppression IoT Monitoring Platform****

**Project Description**

This is a database system developed to monitor and manage IoT-based fire suppression devices across multiple buildings for Brilliant Research Africa (BRA). It securely stores and tracks events, device statuses, locations, and admin access using relational integrity and foreign key constraints. Database Schema Overview The database contains four main tables with specific roles:

**Tables and Their Roles**

• admins: Manages system administrators and technicians. Stores login credentials and roles (e.g. Super Admin, Technician).

• devices: Stores information about all IoT devices (e.g., smoke detectors, heat sensors, sprinklers) installed in buildings.

• events: Logs real-time activities such as temperature readings, alarms, and suppression activations reported by each device. 

• location: Contains information about all monitored buildings and their physical addresses (e.g. headquarters, branches, warehouses)

•  **Relationships**:

 Each device is assigned to a building using the foreign key Building_ID (devices - location).

 Each event is associated with a device using the foreign key Device_ID (events - devices).
Sample Data Summary

Table Records admins 2 devices 5 events 10 location 5

**Admin Roles**: Super Admin, Technician Sample

**Locations**: Kimironko HQ (Yussa Plaza), Makuza Peace Plaza Branch, Masoro Warehouse, CHUK-Kigali Warehouse

**Device Types**:Smoke, Heat, Sprinkler

**Event Types**: Temperature Reading, Alarm, Suppression Activated Sample Advanced SQL Queries

**1. Events in a specific building:**

SELECT e.* FROM events e JOIN devices d ON e.Device_ID = d.Device_ID WHERE d.Building_ID=1;

**2. Latest event per device:**

SELECT * FROM events e WHERE (e.Device_ID, e.Timestamp) IN (SELECT Device_ID, MAX(Timestamp) FROM events GROUP BY Device_ID);

**3. Count of suppression events per device:**

SELECT d.Name, COUNT(*) AS SuppressionCount
FROM events e
JOIN devices d ON e.Device_ID = d.Device_ID
WHERE e.Type = 'Suppression Activated'
GROUP BY e.Device_ID, d.Name;


**4. Buildings with no devices installed:**

SELECT l.Name FROM location l LEFT JOIN devices d ON l.Building_ID=d.Building_ID WHERE d.Device_ID IS NULL;

**5. List of all admins and their roles:**

SELECT Username, Role FROM admins;

**Security and Performance Features**

• Role-Based Access Control (RBAC) with Super Admin and Technician levels

• Foreign key constraints ensure relational integrity

• Indexed primary and foreign keys for faster query performance

• Scalable design capable of handling thousands of events per day

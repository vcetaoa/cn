# **Network Topologies in Cisco Packet Tracer**

![Screenshot](./images/Screenshot%202024-10-22%20004556.png)

---

## **Download Network Topology Packet Tracer File**

You can download the Packet Tracer file containing the network topologies using the link below:

[Download .pkt file](./Topologies.pkt)

---


## 1. Mesh Topology
1. **Open Cisco Packet Tracer**.
2. **Drag** multiple **PCs** and **Switches** (or Routers) into the workspace.
3. **Connect each device to every other device** using **crossover cables**:
   - Use the **`Copper Cross-over` cable** from the **Connections** section.
4. Configure IP Addresses for each PC:
   - Click on **PC** → **Desktop** → **IP Configuration** → Assign an IP Address.
5. **Test connectivity**:
   - Use **ping** from one PC to others: `ping <IP of other PC>`.

---

## 2. Bus Topology
1. **Open Cisco Packet Tracer**.
2. Add **multiple PCs** and **one Hub** from the devices section.
3. **Connect all PCs to the Hub** using **Straight-through cables**.
4. Assign IP addresses to all PCs:
   - Click **PC** → **Desktop** → **IP Configuration** → Set IP Address.
5. **Test the connectivity** by **pinging** other PCs through the **Hub**.

---

## 3. Star Topology
1. **Open Cisco Packet Tracer**.
2. Drag **one Switch** into the workspace.
3. Add **multiple PCs**.
4. **Connect each PC to the Switch** using **Straight-through cables**.
5. Configure IP addresses on all PCs:
   - Click **PC** → **Desktop** → **IP Configuration**.
6. **Test connectivity** between PCs by using the **ping command**.

---

## 4. Ring Topology
1. **Open Cisco Packet Tracer**.
2. Add **multiple Switches** or **PCs** into the workspace.
3. **Connect them in a circular manner** using **Straight-through cables**.
   - Example: PC1 → PC2 → PC3 → PC1.
4. Assign IP addresses to each PC.
5. **Verify the connectivity**:
   - Use **ping** to check if data can travel through the ring from one PC to another.

---

## Notes:
- **IP Address Configuration** is crucial to ensure devices can communicate.
- Use the **ping command** in the **Command Prompt** of each PC to test the network setup.
- Ensure the **cables are correctly connected** (Straight-through for different devices, Crossover for similar devices).
- Use **Simulation Mode** in Cisco Packet Tracer to visualize packet transmission.
"""

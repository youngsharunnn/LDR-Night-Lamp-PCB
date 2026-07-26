## Step 1: Create a New Project

- Open **KiCad** and click **File → New Project...**
- Choose a project directory and enter a project name.
- Click **Save**. KiCad creates the project, schematic (`.kicad_sch`), and PCB (`.kicad_pcb`) files.

### Core Tools & Editors

KiCad provides several integrated tools used throughout the PCB design process:

- **Schematic Editor:** Used to create the circuit schematic by placing symbols and defining electrical connections.
- **Symbol Editor:** Allows you to create or modify schematic symbols that are not available in the default library.
- **PCB Editor:** Used to design the physical PCB, including component placement, trace routing, and board outline creation.
- **Footprint Editor:** Used to create or edit component footprints that represent the physical land patterns on the PCB.
- **Gerber Viewer:** Used to inspect Gerber files before sending them for PCB fabrication.
- **Image Converter:** Converts images (such as JPG or PNG) into KiCad-compatible graphics for adding logos or artwork to the PCB.
- **Calculator Tools:** Provides utilities for calculating resistor values, track widths, via sizes, electrical clearances, and other PCB-related parameters.
- **Drawing Sheet Editor:** Used to customize schematic drawing sheets, including title blocks, borders, and logos.
- **Plugin and Content Manager:** Allows you to install and manage community-developed plugins, libraries, and other KiCad resources.

## Step 2: Draw the Schematic

- Open the **Schematic Editor**.
- Place components using **Add Symbol (A)**.
- Connect components using **Wire (W)**.
- Add **Power Symbols (P)** such as **VCC** and **GND**.
- Edit component properties and assign values where necessary.

## Step 3: Annotate the Schematic

- Click **Annotate Schematic**.
- Allow KiCad to automatically assign reference designators (**R1, C1, U1**, etc.) to all components.

## Step 4: Organize & Review the Schematic

- Complete the **Title Block** with details such as the project name, revision, date, and author using **File → Page Settings**.
- Use **Text** and **Graphics** tools to label and group different sections of the circuit for better readability.
- Replace long wires with **Net Labels** to keep the schematic clean and organized.
- Mark intentionally unused pins with the **No Connection Flag** to avoid unnecessary ERC warnings.
- Optionally, add **logos** or **hyperlinks** for better project documentation.

### Step 5: Run Electrical Rules Check (ERC)

- Click **Electrical Rules Checker (ERC)**.
- Review and fix errors or warnings such as unconnected pins or missing power flags.

## Step 6: Assign Footprints

- Open **Assign Footprints**.
- Select an appropriate physical footprint for each schematic symbol.

### Understanding Footprint Naming

A typical footprint name (e.g., `Resistor_THT:R_Axial_DIN0207_L6.3mm_D2.5mm_P15.24mm_Horizontal`) contains important information:

- **DIN Code:** The industry-standard size code (e.g., **DIN0207**).
- **L (Length):** The length of the component body.
- **D (Diameter):** The diameter of the component body.
- **P (Pitch):** The distance between the component leads or solder pads. This is the most critical dimension for ensuring the component fits the PCB correctly.
- **Orientation:** Indicates whether the component is mounted **Horizontally** or **Vertically**.

### Handling Missing Footprints

If a specific component does not have a dedicated footprint:

- Choose a compatible footprint with the same **pitch** and similar physical dimensions (e.g., using a **2-pin header** footprint for a 2-lead microphone).
- If no suitable footprint is available, create a custom footprint using the **Footprint Editor**.
- Save the footprint assignments.

## Step 7: Transfer the Schematic to the PCB

- Open the **PCB Editor**.
- Click **Update PCB from Schematic (F8)**.
- Import all assigned footprints into the PCB layout.

## Step 8: Configure the PCB Layout

Before starting the PCB layout, familiarize yourself with the PCB layers and configure the board settings.

### Understanding PCB Layers

- **F.Cu / B.Cu:** Front and back copper layers used for electrical connections.
- **F.Mask / B.Mask:** Defines openings in the solder mask for exposed pads.
- **F.SilkS / B.SilkS:** Printed text, logos, and component outlines.
- **F.Paste / B.Paste:** Solder paste stencil layers for automated assembly.
- **F.Courtyard / B.Courtyard:** Component clearance areas to prevent overlap during assembly.
- **Edge.Cuts:** Defines the physical shape and boundary of the PCB.
- **Margin:** Specifies safe clearance areas near the board edge.
- **F.Fab / B.Fab:** Fabrication information used by manufacturers.

### Configure Design Constraints

Design constraints define the manufacturing limits of your PCB and help prevent fabrication errors. Configure these settings in **Board Setup** according to your PCB manufacturer's capabilities.

Common values supported by most manufacturers include:

| Constraint | Recommended Value |
| --- | --- |
| Minimum Clearance | 0.15 mm |
| Minimum Track Width | 0.15 mm |
| Minimum Connection Width | 0.15 mm |
| Minimum Annular Width | 0.10 mm |
| Minimum Via Diameter | 0.50 mm |
| Copper to Hole Clearance | 0.25 mm |
| Copper to Edge Clearance | 0.25 mm |
| Minimum Through Hole | 0.30 mm |
| Hole to Hole Clearance | 0.25 mm |
| Minimum Item Clearance | 0.15 mm |
| Minimum Text Height | 0.80 mm |
| Minimum Text Thickness | 0.08 mm |

### Configure Trace Widths

- Use KiCad's **Calculator Tools** to determine the required track width based on the expected current.
- In **Board Setup**, define commonly used track widths (e.g., **0.3 mm** for signal traces and **0.5 mm** for power traces).

### Configure Net Classes

- Create **Net Classes** in **Board Setup** or **Schematic Setup** to group nets with similar routing rules.
- Assign wider traces and larger clearances to **Power** nets (e.g., **VCC**, **GND**) and standard values to **Signal** nets.
- These settings synchronize between the schematic and PCB editor, ensuring consistent routing throughout the design.

## Step 9: Define the Board Outline

- Select the **Edge.Cuts** layer in the PCB Editor.
- Use the **Line**, **Rectangle**, **Arc**, or **Circle** tools to draw the physical shape of the PCB.
- Ensure the board outline forms a **closed, continuous shape** with no gaps or overlapping edges.
- Set the board dimensions according to your project requirements.
- Save the PCB layout before proceeding to component placement.

## Step 10: Arrange Components

- Move and position all footprints within the board outline.
- Arrange components logically to simplify routing and optimize the layout.

### Working with Ratlines

- **Ratlines** are thin lines that indicate electrical connections that still need to be routed.
- Use the **Ratline Visibility** controls to:
    - Toggle all ratlines on or off.
    - Display ratlines only for the selected component to reduce visual clutter while positioning parts.

### Aligning and Distributing Components

- Select multiple components and use **Right-Click → Align** to align them along a common edge.
- Use **Right-Click → Distribute** to evenly space components horizontally or vertically for a cleaner layout.

### Adding External 3D Models (Optional)

If a footprint does not include a 3D model:

- Download a compatible **.step** or **.stp** model from sources such as **GrabCAD**.
- Open the footprint **Properties → 3D Models** tab.
- Add the model and adjust its **Offset**, **Scale**, and **Rotation** until it aligns correctly with the footprint.

## Step 11: Route the PCB

- Use **Route Tracks (X)** to connect component pads according to the schematic.
- Follow the **ratlines** to complete all required electrical connections.
- Use appropriate **track widths** based on the assigned net classes (e.g., wider tracks for power, narrower tracks for signals).
- Add **vias** when routing between different copper layers, if necessary.

### Professional Trace Routing

- Use **45° trace angles** whenever possible, as they are the industry standard and KiCad's default routing style.
- Avoid **90° corners**, as they can negatively affect signal integrity and are less desirable for manufacturing.
- For high-speed or professional designs, use **Track Fillets** to create smooth curves:
    1. Select a track segment.
    2. **Right-click → Fillet**.
    3. Enter the desired fillet radius (e.g., **5 mm**).
- Keep traces as short and direct as possible while maintaining the required clearances from other copper features and the board edge.
- Save the PCB layout after completing the routing.

## Step 12: Add a Copper Pour (Optional)

- Select **Add Filled Zone** from the right toolbar.
- Choose the appropriate copper layer (e.g., **F.Cu**) and assign it to a net, typically **GND**.
- Draw the zone boundary around the PCB or the desired area.
- Refill the zone to generate the copper pour.
- Verify that the copper pour is connected correctly and does not create clearance violations.

## Step 13: Run Design Rules Check (DRC)

- Click **Design Rules Checker (DRC)**.
- Review and fix errors such as clearance violations, unconnected nets, overlapping tracks, or missing connections.
- Ensure the PCB satisfies all design constraints before proceeding.

## Step 14: Add Graphics & Branding (Optional)

You can add logos and custom graphics to make your PCB look more professional and easier to identify.

### Add Custom Graphics

- Open the **Image Converter** from the KiCad Project Window.
- Load your logo or image and resize it to fit the PCB.
- Adjust the **Black/White Threshold** if needed for a cleaner graphic.
- Set the **Board Layer** to **Front Silk Screen (F.SilkS)** and the **Output Format** to **Footprint**.
- Export the graphic and paste it into the **PCB Editor** on the **F.SilkS** layer.
- To hide the auto-generated reference text, edit the footprint and disable the **Reference Designator** display.

### Use Built-in Logos and Graphics

- Use **Add Footprint** and search for **"Logo"** to access KiCad's built-in logos (e.g., KiCad, FCC, Open Source Hardware, WEEE).
- Use **Change Side / Flip** to move graphics between the front and back of the PCB.
- Add text, version numbers, or simple shapes using the **Text** and **Graphics** tools on the silkscreen layers.

## Step 15: Inspect the PCB in 3D

- Open the **3D Viewer** from the **PCB Editor**.
- Verify the overall appearance of the PCB, including the board outline, component placement, and orientation.
- Check for any mechanical interference, missing or incorrectly aligned components, and ensure all 3D models are positioned correctly.
- Rotate, pan, and zoom the model to inspect the board from different angles.
- Make any necessary adjustments in the **PCB Editor** before generating the manufacturing files.

## Step 16: Generate Manufacturing Files

Generate all files required for PCB fabrication, assembly, and project documentation.

- **Generate Gerber Files** to produce the manufacturing layers for PCB fabrication.
- **Generate Drill Files** to define the locations and sizes of all drilled holes.
- **Generate Bill of Materials (BOM)** listing all components used in the design.
- **Generate Position (Pick-and-Place) Files** containing component locations and orientations for automated assembly.
- **Export the Schematic and PCB** as PDF files for documentation and review.
- **Generate a STEP (.step) File** to create a 3D model of the PCB for mechanical design and enclosure integration.
- Verify that all generated files are saved correctly and are ready to be shared with the PCB manufacturer or assembly service.

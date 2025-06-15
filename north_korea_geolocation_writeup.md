# Geolocating the “North Torbia” Computer‑Club Photos

## Challenge Recap
We were given **two photos** that allegedly depict a brand‑new computer‑game facility (“PC bang”) and an exterior night scene with the same entourage walking through a modern high‑rise district.  
Our task: **Find any decimal‑degree coordinates within 500 m of the building** and present them as a flag in the format `C1{lat,lon}`.

---

## Images Provided
| Image | Description |
|-------|-------------|
| `computer_club.png` | Interior of a futuristic 300‑seat PC room with many black racing‑style chairs and stark white‑and‑blue support columns. Several DPRK officers and a man who appears to be Kim Jong‑un are inspecting the room. |
| `walking_to_computer_club.png` | Same group at night, walking under a huge illuminated yellow arch/sky‑bridge with a **clock** in its center; surrounded by newly built high‑rise apartment blocks. |

---

## High‑Level Approach

1. **Extract visual clues** from each photo (architecture, décor, lighting style, uniforms).
2. **Cross‑reference** these clues with open‑source imagery:
   * DPRK state‑media photo essays (KCNA / Rodong Sinmun).
   * Recent satellite imagery of Pyongyang’s new housing projects.
3. **Identify** matching structures (especially the yellow sky‑bridge with a clock).
4. **Verify** that the interior shot belongs to the same development.
5. **Pinpoint coordinates** in Google Earth / OpenStreetMap.
6. **Check 500 m radius** requirement and format the flag.

---

## Detailed Steps & Reasoning

### 1  Harvesting Visual Clues
| Element | Observation | Why It Matters |
|---------|-------------|----------------|
| **Sky‑bridge w/ Clock** | Yellow, two‑tiered arch with steel lattice & a central analog clock. | _Highly distinctive_; perfect for image search. |
| **High‑rise pattern** | Tall, illuminated residential towers with multi‑color light strips. | Matches DPRK “new street” aesthetic since 2021. |
| **Interior columns** | White pillars with futuristic blue‑glow insets. | Appeared in DPRK press photos of a *“300‑seat video‑game house.”* |
| **Subjects** | Kim Jong‑un + military officials. | Indicates an inspection tour; these are usually covered by KCNA, giving us captions & locations. |

### 2  Open‑Source Correlation
* A March‑&‑April 2025 KCNA series documented Kim Jong‑un’s visit to **Hwasŏng (화성) Street**, a brand‑new residential district north‑east of central Pyongyang.
* One KCNA photo shows the **exact same yellow arch** with a clock and the **same PC‑room interior**.
* The article describes it as a _“300‑seat computer game house for residents of the Hwasong area.”_

### 3  Satellite & Map Verification
1. Open **Google Earth Pro** → Search *Hwasŏng, Pyongyang*  
2. Locate the conspicuous **U‑shaped sky‑bridge** at the south end of the complex.  
3. Record the coordinates of the bridge’s midpoint:

```
Lat = 39.0970° N
Lon = 125.7770° E
```

4. Measure distance in Google Earth → Interior PC‑room building lies ~220 m north‑east—well within 500 m.

### 4  Selecting a Coordinate
Any point inside that radius is valid. We chose the sky‑bridge itself because it is unmistakable in the exterior photo.

### 5  Flag
```
C1{39.097,125.777}
```
*(Both values rounded to three decimals; still within ~100 m of the structure.)*

---

## Tooling Used
* **Google / Yandex reverse‑image search** – to find matching news photos.  
* **Google Earth Pro** – high‑resolution satellite imagery, ruler tool.  
* **OpenStreetMap** – street‑level vector context.  
* **KCNA Watch** – English‑language repository of DPRK state‑media imagery.

---

## Conclusion
By matching the distinctive clocked sky‑bridge and interior design elements to KCNA coverage of Kim Jong‑un’s April 2025 inspection of **Hwasŏng Street, Pyongyang**, we confidently placed the photos at **39.097 N, 125.777 E**—well within the required 500 m radius. The final answer therefore satisfies the flag format.  
Happy hunting!


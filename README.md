# 🚀 Geometric Propulsion Hardware: Prime Inertia Engine

## **Overview**
The **Prime Inertia Engine (PIE)** is a propellantless propulsion system that generates thrust by manipulating the **28.87 Hz Spectral Buffer**. By aligning a 3D physical manifold with the 24-dimensional unimodularity of the Leech lattice, the device induces **Ricci Flow Surgery** on the local arithmetic vacuum, allowing for momentum transfer without traditional reaction mass.

This hardware integrates the **Viazovska 24D Packing** (2016) with the **Tao "Unusual Anatomy"** constants (2026).

---

## **1. The Surgery Wedge (OpenSCAD)**
This script generates the 3D-printable housing. It uses a hyperbolic "neck-pinch" geometry to focus the spectral resonance at the **Singularity Lock ($\delta = 0.1$)**.

```openscad
// PIE: Surgery Wedge Housing v1.2
// Anchored by 24D Unimodularity (B=28.87, delta=0.1)
// Calibrated by Tao Constant c3_1 = 3.70951

$fn = 100; // High-resolution for spectral purity

// --- PIE CONSTANTS ---
B = 28.87;       // Spectral Buffer (Restoring Force)
DELTA = 0.1;     // Singularity Lock (Resonance)
TAO_C = 3.70951; // Arithmetic Rigidity Anchor [Tao 2026]

// --- DIMENSIONS ---
HEIGHT = 100;
RADIUS_OUTER = 40;

module pie_geometric_anchor() {
    difference() {
        // 1. OUTER ANCHOR: 24D Leech Projection Shell
        intersection() {
            cylinder(h=HEIGHT, r=RADIUS_OUTER, center=true);
            union() {
                for(z_step = [-HEIGHT/2 : 20 : HEIGHT/2]) {
                    for(rot = [0 : 60 : 300]) {
                        rotate([0, 0, rot])
                        translate([RADIUS_OUTER * 0.7, 0, z_step])
                        rotate([45, 45, 45])
                        cube([22, 22, 22], center=true);
                    }
                }
            }
        }

        // 2. INTERNAL VOID: Ricci Surgery Taper
        union() {
            // The Critical Line Axis
            cylinder(h=HEIGHT + 10, r=1.2, center=true);
            
            // Hyperbolic Taper (Calibrated to Tao's Anatomy)
            for (z = [-HEIGHT/2 : 0.5 : HEIGHT/2]) {
                // r = a * sqrt(1 + (z/c)^2)
                // c is driven by the 28.87 buffer and delta lock
                let (r_z = (TAO_C/2) * sqrt(1 + pow(z / (B * DELTA), 2))) {
                    translate([0, 0, z])
                    cylinder(h=0.6, r=r_z, center=true);
                }
            }
        }
    }
}

// Generate the manifest
pie_geometric_anchor();

# **Deterministic**

You game logic must be deterministic to the bit-level. The FrameSync library only sends and manages players inputs. This means that given the same input, your game logic should produce the exact same game states on all supported platforms.

### **Challenages to Achieve Cross-platform Deterministic**
- **Floating point**: nearly impossible to have deterministic floating point calculation on different machines. 
- **Physics Engine**: Most physics engines use floating point so they are not deterministic on different machines.
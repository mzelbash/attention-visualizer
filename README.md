# Attention Windows

An interactive, single-file web app that shows how four attention mechanisms decide which tokens a query is allowed to look at. It was built for **SEAS 8525: Computer Vision and Generative AI** at George Washington University.

The app explains attention visually instead of with long text. Students click a token or an image patch and immediately see which keys and values it attends to, how strongly, and how much computation each mechanism needs.

## Mechanisms covered

| Mechanism | Idea | Matrix shape |
|---|---|---|
| **Global** | Every token sees every token. | Full square |
| **Masked (causal)** | Score everything, then hide the future. | Lower triangle |
| **Fixed window** | Only look inside your own block (Swin style). | Block diagonal |
| **Quadrangle** | Look inside a learned, tilted window (vision only). | Content-shaped regions |

## Features

1. **Full attention matrix.** Every row is filled, so each mechanism shows its own recognizable pattern. The selected query row is outlined, and cells fade smoothly when you switch mechanisms.
2. **Two views.**
   1. **Sentence:** the 8-token sentence *"the cat sat on the mat and slept"*, with attention arcs and weight bars under each token.
   2. **Image:** a built-in sample scene split into patches, with each patch tinted by its attention weight. You can upload your own image and choose a 3×3, 4×3, 4×4 or 6×4 grid.
3. **Three cell states.** Attended (blue, by weight), computed then masked (red hatching), and never computed (grey). This separates causal masking, which computes every score and then discards some, from windowed attention, which never computes them.
4. **Scores computed counter.** Shows how many QKᵀ entries each mechanism calculates out of N², and how many are masked in causal attention.
5. **Shifted windows toggle.** Shows how Swin Transformer moves window borders so information can cross between blocks.
6. **Quadrangle sliders.** Rotation, skew and scale controls deform the window live in the image view.
7. **Masking question.** In causal mode, a reveal-answer card explains why future scores are set to −∞ (in code, a large negative number such as −1e9) instead of 0, using the softmax formula.
8. **Rendered math.** The attention and softmax formulas are drawn with native MathML, so no math library is needed.
9. **Light, dark and system themes.** Each browser remembers its own choice.

## Getting started

No installation or build step is needed.

1. Clone or download this repository.
2. Open `attention_windows.html` in any modern browser (Chrome, Edge, Firefox or Safari).

To publish it online, enable **GitHub Pages** for the repository and open the page at
`https://<your-username>.github.io/<repo-name>/attention_windows.html`.

## How to use 

1. Pick a mechanism with the buttons at the top. Each button shows a thumbnail of its matrix pattern.
2. Click any token, patch or matrix row to make it the query.
3. Switch between **Sentence** and **Image** to compare text and vision.
4. In **Fixed window**, toggle **Shifted windows** to show how Swin connects neighboring blocks.
5. In **Quadrangle** (image view), drag the sliders and watch which patches are kept.
6. In **Masked (causal)**, ask the class the masking question before revealing the answer.
7. Press **?** next to the mechanism name for a short explanation and the models that use it.

## Notes on accuracy

1. The attention weights are **illustrative**, not taken from a trained model. Each row is a proper softmax and sums to 1.
2. The query vector is never restricted in any mechanism. Only the keys and values change.
3. Quadrangle attention is simplified. The real method predicts a transform for each window from the image content and bilinearly samples keys and values inside the warped shape. The app approximates this by keeping patches whose centers fall inside the quadrangle.
4. Causal attention on images appears only in autoregressive generators such as ImageGPT, which read patches in raster order (p0, p1, p2 and so on).

## References

1. Vaswani et al., *Attention Is All You Need*, NeurIPS 2017.
2. Liu et al., *Swin Transformer: Hierarchical Vision Transformer using Shifted Windows*, ICCV 2021.
3. Zhang et al., *Vision Transformer with Quadrangle Attention*, 2023.
4. Chen et al., *Generative Pretraining from Pixels* (ImageGPT), ICML 2020.

## Author

**Dr. Mohamed Elbasheer**
School of Engineering and Applied Science, George Washington University
SEAS 8525: Computer Vision and Generative AI

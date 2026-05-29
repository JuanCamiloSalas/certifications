[![](https://img.shields.io/badge/<_SAA-FF4859?style=for-the-badge)](../README.md)

# 🖼️ Assets (`assets/`)

> Diagrams, screenshots, and any image referenced by a card or comparison.

## Rules

- **Add an image only when it actually helps.** A picture that just decorates a card is noise.
- **File name = self-describing.** `vpc-public-private-subnets.png`, not `image1.png`.
- **Reference from a card with a relative path:**
  ```markdown
  ![alt text](../../assets/<file>.png)
  ```
- **Prefer images already in AWS docs / AWS blogs.** Most diagrams from the course have a public equivalent — saves you the screenshot work.
- **For original drawings:** mobile photos of hand-drawn diagrams from the notebook are fine, just crop and rename.

## Suggested subdivisions (optional)

If the folder grows, split by block:

```
assets/
├── 03-elb-asg/
├── 06-s3-avanzado/
├── 15-vpc/                  ← VPC will be the heaviest
└── ...
```

Don't pre-create subfolders. Make them only when you have ≥ 3 images per block.

---

[![](https://img.shields.io/badge/<_SAA-FF4859?style=for-the-badge)](../README.md)

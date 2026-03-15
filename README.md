# AI Checker

[English] | [中文](README.zh.md)

A Claude Code Skill for detecting AI-generated content across text, images, video, audio, and documents — with a confidence scoring framework and structured report template.

## Features

| Target | Detection Techniques |
|--------|---------------------|
| **Text / Articles** | Perplexity, Burstiness, N-gram distribution |
| **Images** | GAN checkerboard artifacts, ELA error analysis, FFT/DCT frequency domain, EXIF metadata, C2PA |
| **Video Deepfakes** | Facial Feature Drift (FFD), temporal frequency artifacts, optical flow analysis, lip sync |
| **Synthetic Audio** | Mel spectrogram, MFCC, LFCC, SSL feature fusion (Wave2Vec2BERT) |
| **PDF Documents** | Metadata forensics, ELA analysis, incremental update detection, font consistency |
| **Links / Bot Traffic** | Bot behavioral signatures, JS fingerprinting, honeypot detection |

## Confidence Scoring Framework

```
Confidence = (strong_evidence × 3 + medium_evidence × 1.5 + auxiliary_evidence × 0.5)
           ÷ (max_strong × 3 + max_medium × 1.5 + max_auxiliary × 0.5)

≥ 0.75   → High confidence: AI-generated
0.50–0.74 → Medium confidence: likely AI-assisted, review recommended
0.25–0.49 → Low confidence: suspicious but insufficient evidence
< 0.25   → Likely human-authored
```

## AI Content Statistics (March 2025)

- **74.2%** of newly published web pages contain AI content (Ahrefs, 900K page sample)
- **52%** of online articles are AI-written (Graphite SEO 2025)
- **~57%** of all online text is AI-assisted or AI-generated (composite estimate)
- **~90%** predicted by 2026 (Europol)

## Installation

### Option 1: Import the `.skill` file

```bash
curl -L https://github.com/chat2dev/ai-checker/raw/main/ai-content-detection.skill \
  -o ai-content-detection.skill
```

Then import the `.skill` file in Claude Code settings.

### Option 2: Copy SKILL.md manually

Copy `ai-content-detection/SKILL.md` to `~/.claude/skills/ai-content-detection/`.

## Trigger Examples

The skill activates automatically on queries like:

- "Is this article AI-written?"
- "Check if this image is AI-generated"
- "Is this audio clip a synthetic voice?"
- "I suspect this PDF income statement is forged"
- "How much of the internet is AI-generated?"
- "My thesis was flagged as AI — how do I prove it's mine?"
- Detecting deepfakes, AI writing, synthetic voices, document fraud

## Benchmark Results

Validated across 8 scenarios (including HC3, ASVspoof, and FaceForensics++ dataset patterns):

| Configuration | Pass Rate | Token Usage |
|--------------|-----------|-------------|
| With Skill | **100%** (40/40) | ~29,320 |
| Without Skill | 85% (34/40) | ~19,385 |
| **Delta** | **+15pp** | +9,935 |

The skill's unique value lies in: the confidence scoring formula, precise statistical data references, three-tier evidence classification, and PDF incremental update detection.

## File Structure

```
ai-checker/
├── README.md
├── README.zh.md                       # Chinese version
├── ai-content-detection.skill        # Packaged skill file (ready to import)
└── ai-content-detection/
    └── SKILL.md                      # Skill source
```

## Use Cases

- Content moderators verifying submission authenticity
- Bank / financial compliance teams identifying forged documents
- Academic institutions handling AI plagiarism disputes
- News editors verifying suspected deepfake video/audio
- Researchers measuring AI content prevalence
- Individuals proving their work is not AI-generated

## License

MIT

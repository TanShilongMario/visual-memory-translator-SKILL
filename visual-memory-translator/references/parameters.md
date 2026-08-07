# Full Parameter Schema

```yaml
skill: visual_memory_translator

original_display_mode:
  # split_top_bottom
  # split_left_right
  # translation_only
  # taped_corner_photo
  # pinned_photo
  # paperclip_photo
  # polaroid_insert
  # film_strip
  # exhibition_reference
  # stamp_window
  # ticket_image
  # vellum_overlay
  # peek_window

layout_mode:
  # split_editorial
  # large_whitespace_small_art
  # center_art_annotations
  # editorial_cards
  # single_artwork
  # asymmetric_archive

style_mode:
  # minimal_watercolor
  # minimal_line_watercolor
  # freehand_doodle
  # minimal_vector
  # single_line_sketch
  # extreme_minimal_abstraction
  # memory_color_blocks
  # structural_deconstruction
  # stamp_memory
  # exhibition_ticket
  # fluted_glass
  # archive_card
  # specimen_sheet
  # map_note
  # commemorative_cover

abstraction_level:
  # low | medium | high | extreme

whitespace_level:
  # medium | high | very_high

translation_scale:
  # small | one_ninth_grid | medium

text_mode:
  # none | user_text | auto_poetic | auto_reflective
  # auto_travel_note | auto_exhibition_label | auto_minimal

text_content:  # optional

doodle_level:
  # none | very_low | low

background_style:
  # warm_off_white_paper | ivory_paper | cool_white_paper | custom

transition:
  # deckled_paper_edge | clean_cut | soft_fade
  # vellum_overlap | mask_window | paper_fold | no_visible_separator

ratio:
  # 3:4 | 1:1 | 4:3 | 3:2 | 16:9 | 9:16 | custom
```

---

## Recommended Default Configuration

```yaml
skill: visual_memory_translator
preset: default_editorial_memory

original_display_mode: auto
layout_mode: auto
style_mode: auto
abstraction_level: high
whitespace_level: very_high
translation_scale: one_ninth_grid
text_mode: auto_poetic
doodle_level: very_low
background_style: warm_off_white_paper
transition: deckled_paper_edge
ratio: 3:4
```

`auto` 的决策规则见 [defaults-and-presets.md](defaults-and-presets.md)。

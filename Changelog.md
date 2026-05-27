# Changelog

## v2 — May 2026
- Fixed XML closing tag in Check Outline Criteria node
  (</criteria> was malformed in v1)
- Fixed <outline> tag spelling in Check Outline Criteria
  (<ouline> corrected to <outline>)
- Fixed typo in Generate Outline node
  (well-structure → well-structured, abut → about)
- Fixed typo in Expand Outline Sections node
  (relevent → relevant)
- Fixed typo in Refine and Polish Documents node
  (polisted → polished)
- XML tag fixes improve LLM parsing reliability
  in the quality gate evaluation

## v1 — May 2026
- Initial release
- Multi-stage document generation pipeline
- Quality gate with PASS/FAIL conditional routing
- Three-phase LLM chain: outline → expand → polish
- Five quality criteria enforced before expansion
- OpenRouter with GPT-4.1
- Failure handling with explanation output

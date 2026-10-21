# codex-imagegen-skill

**Codex 전용** 이미지 생성·편집 스킬입니다. (A Codex-only skill for generating and editing raster images. Not for Claude Code.)

사진·일러스트·텍스처·스프라이트·목업 같은 래스터 이미지를 새로 만들거나 기존 이미지를 편집합니다.

## 동작 방식
- **기본 경로**: Codex 내장 `image_gen` 도구. `OPENAI_API_KEY`가 필요 없습니다.
- **대체 경로(CLI)**: 사용자가 명시적으로 요청할 때만 `scripts/image_gen.py`(`generate`, `edit`, `generate-batch`)를 씁니다. `OPENAI_API_KEY`와 `openai` SDK가 필요하며 API 비용이 발생합니다.
- **투명 배경**: 평면 크로마키 배경으로 생성한 뒤 `scripts/remove_chroma_key.py`로 로컬에서 제거합니다. 진짜 투명도가 필요하면 CLI 경로를 사용자에게 확인합니다.
- 생성 파일은 기본적으로 `$CODEX_HOME/generated_images/` 아래에 저장되므로, 프로젝트에서 쓸 에셋은 작업 폴더로 복사합니다. 기존 파일은 덮어쓰지 않고 새 이름으로 저장합니다.

## 설치
```bash
git clone https://github.com/Kein-chronicle/codex-imagegen-skill.git ~/.codex/skills/imagegen
```
Codex에서 `$imagegen` 으로 호출합니다. CLI 경로를 쓰려면 `uv pip install openai pillow` 가 필요합니다. API 키는 환경 변수로만 설정하고 파일에 적지 마세요.

## 구성
| 경로 | 내용 |
|---|---|
| `SKILL.md` | 스킬 본체(모드 선택 규칙, 워크플로, 투명 배경 처리) |
| `scripts/image_gen.py` | CLI 대체 경로 |
| `scripts/remove_chroma_key.py` | 크로마키 배경 제거 |
| `references/` | 프롬프트 가이드, 샘플 프롬프트, CLI·API·네트워크 참고 |
| `agents/openai.yaml`, `assets/` | Codex 표시용 메타데이터와 아이콘 |

## 출처와 라이선스
이 스킬의 폴더 구조와 라이선스는 OpenAI가 공개한 Codex `imagegen` 시스템 스킬(https://github.com/openai/skills, `skills/.system/imagegen`, Apache-2.0)과 같은 형식입니다. 번들된 [`LICENSE.txt`](LICENSE.txt)는 Apache License 2.0이며 변경하지 않았습니다. 재배포·수정 시 이 라이선스와 고지를 유지하고 수정 내용을 표기하세요.

## 주의
- Codex 전용입니다. Claude Code 등 다른 에이전트에서는 `image_gen` 도구가 없어 동작하지 않습니다.
- 생성된 이미지의 권리와 사용 조건은 사용하는 서비스의 약관을 따릅니다.

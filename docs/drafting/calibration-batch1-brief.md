# Drafting brief: calibration batch 1 (20 new seed cards)

Written 19 November 2026 for WP1.2 (calibration pool to 30). This file is the `prompt_ref` of every card drafted from it. Calibration cards are never used as test items.

## What a drafter must read first

1. `docs/seed-spec-v2.md` in full (card format, span rules, licence rules, linter rules).
2. Two reference cards in full: `data/seeds_v2_draft/D02_social_norm_library.json` (decision family) and `data/seeds_v2_draft/C01_calver_compare.json` (code family). Copy their structure, not their content.
3. `data/registry/relation_families.json` and `data/registry/domains.json`. Use only ids that exist there.
4. `src/seed_lint_v1.py` (`IMPLIED_BANNED`, `CUE_PHRASES`) so implied-cue variants contain no role-stating phrase.

## Hard requirements for every card

- File `data/seeds_v2_draft/<id>.json`, `schema` `seed-card-v2`, `status` `draft`, `author_id` `tanjamul`, `created` and `updated` `2026-11-19`, `split` null, `contamination` `{"status": "not run"}`.
- `model_assistance` `drafted`, with `model_assistance_log`: `model` (your exact model id), `date` 2026-11-19, `scope` (which fields you wrote: all of them), `prompt_ref` `docs/drafting/calibration-batch1-brief.md`, `human_edits` null.
- `template_group_id` `TG-<id prefix>` (for example `TG-D06`); `provenance_group_id` a short `PG-` id for the source case.
- Six core variants: analogy, requirement and counter, each with a `stated` and an `implied` cue, all `full` fit. List every other role x fit cell in `cells_not_applicable` with a one-sentence reason (follow D02's reasons). Optional: one stated and one implied `partial` or `wrong` fit analogy variant if a natural one exists.
- `turns` `["single", "multi"]`. `human_review` with empty `reviewers` and a null annotator pair per variant (copy D02's shape).
- At least two valid answers and at least two `minimal` invalid answers per variant, plus one `copy` answer. Each minimal invalid answer is one edit away from a valid one and fails exactly the checks it lists.
- **Bans by conflict, not by decree.** Every source detail that is MUST_NOT under an implied cue must conflict with a fact of the target (another currency, unit, name, interface, number). Put that conflicting fact in the target task or rules, so the ban is checkable. A detail whose copying would merely be odd is MAY or UNCLEAR, never MUST_NOT.
- Detail units (`incidental_details`) need detectors (`leak_terms` or `leak_regex`) that occur in the example and nowhere in the target task, rules, format or the variant's own words. At least one detail has a `control` swap (as I5 in D02).
- Code cards: `func` and `tests` as in C01; every valid answer must pass the tests and every check; run them.
- Run `python -I src/seed_lint_v2.py data/seeds_v2_draft/<id>.json` until it shows 0 errors. Warnings are allowed if you write why in the card's `notes`. Then run `python -I src/export_v2.py data/seeds_v2_draft/<id>.json --positions start,middle,end` and make sure it exports without error.
- Use `scripts/spans_from_markup.py` to build `source_spans` from markup if it helps.

## Quality bar (the supervisor asked for striking, real-world items, not easy synthetic ones)

- **Targets are real tasks a Bangladeshi student, teacher, office or small business would actually ask a chat model for**: Dhaka, Chattogram, Sylhet, BDT, bKash, local universities, garment factories, hostels, courier firms. Concrete numbers in the brief.
- **User words sound like a real person typing**, not like a template: short, a little informal, a reason for sharing the example ("my senior sent me this", "our IT guy keeps quoting this"). No phrases such as "Please leverage", "comprehensive", "delve". No em dashes anywhere in the card.
- **The example is worth sharing**: 120 to 250 words for `standard` length. A documented case states only facts that its cited paper or page supports; give a DOI or URL. Do not invent numbers for a real study. If you are not sure of a fact, leave it out.
- The same task must be solvable without the example (the no-example condition must be possible), and the role sentence must change what a correct answer looks like.
- Each card must have a relation that is not trivial to copy: the analogy role should need the idea moved into another domain.

## The 20 seeds

| ID | Family | Relation family | Target domain | Source example | Source type | Target task (sketch) |
| --- | --- | --- | --- | --- | --- | --- |
| D06_default_enrolment_welfare | decision | default_option_nudge | human_resources | Automatic enrolment in US 401(k) retirement plans raised participation sharply (Madrian and Shea, QJE 2001, doi 10.1162/003355301753265543) | documented_case | Design enrolment for a Dhaka software firm's new staff welfare fund (contribution in BDT, opt-out window, payroll dates) |
| D07_commitment_savings_eid | decision | commitment_device | community_and_nonprofit | SEED commitment savings accounts in the Philippines (Ashraf, Karlan and Yin, QJE 2006, doi 10.1162/qjec.2006.121.2.635) | documented_case | A Mirpur shopkeepers' cooperative wants members to save for Eid through bKash; design the scheme |
| D08_random_audit_canteen | decision | random_spot_audit | hospitality_and_events | Raising the audit probability for village road projects in Indonesia reduced missing expenditure (Olken, JPE 2007, doi 10.1086/517935) | documented_case | Plan hygiene inspections for 12 campus canteen stalls with 2 inspectors |
| D09_deferred_acceptance_supervisors | decision | deferred_acceptance_matching | teaching_and_learning | New York City high-school match redesign (Abdulkadiroglu, Pathak and Roth, AER P&P 2005, doi 10.1257/000282805774670167) | documented_case | Assign 60 final-year CSE students to 12 thesis supervisors with capacities |
| D10_checklist_changeover | decision | checklist_standardisation | manufacturing | WHO Surgical Safety Checklist study (Haynes et al., NEJM 2009, doi 10.1056/NEJMsa0810119) | documented_case | Reduce errors at style changeover on sewing lines in a Gazipur garment factory |
| D11_lottery_concert_seats | decision | allocation_by_lottery | hospitality_and_events | Original: a university robotics club allocates scarce GPU-server slots by a weekly lottery among eligible teams | original_scenario | Allocate 400 hall seats for a campus concert among 2,300 student requests |
| D12_buffer_slots_clinic | decision | capacity_buffer | healthcare_services | Original: a busy Old Dhaka biryani house keeps two tables unbooked each evening for walk-in regulars | original_scenario | Plan daily appointment slots for a university medical centre's single doctor |
| D13_oncall_rotation | decision | duty_rotation | it_operations | Original: a Chattogram newspaper rotates the night news editor weekly so no one burns out and everyone knows the desk | original_scenario | Plan night on-call for a 5-person IT team at a private hospital |
| D14_slab_quota_wifi | decision | increasing_block_tariff | telecommunications_and_networks | Original summary of slab-based residential electricity pricing: low price for the first block, higher per-unit price above it | original_scenario | Price monthly Wi-Fi data for hostel residents so light users pay little and heavy users pay for bandwidth |
| D15_feedback_water_dorm | decision | personal_feedback_loop | environment_and_conservation | Original: dynamic "your speed" roadside signs that show each driver their own speed slow traffic | original_scenario | Cut water waste in a 300-student dorm with one meter per floor |
| C06_backoff_sms_gateway | code | retry_with_backoff | banking_and_payments | AWS Architecture Blog, "Exponential Backoff And Jitter" (Brooker, 2015) | software_practice | Python function that returns the retry delays for a bank's OTP SMS sender |
| C07_idempotent_orders | code | idempotent_operation | retail_and_ecommerce | Stripe API docs on idempotent requests (idempotency keys) | software_practice | Python function that records an online-shop order so double submissions do not create two orders |
| C08_phone_key_courier | code | canonical_key_normalisation | logistics_and_delivery | Original: a mailing-list tool lower-cases emails and strips spaces before checking duplicates | original_scenario | Python function that normalises Bangladeshi mobile numbers (+880, 880, 01...) for a courier's customer de-duplication |
| C09_token_bucket_otp | code | token_bucket_rate_limiting | security_and_access_control | Token bucket algorithm as documented for API rate limiting (cite a vendor or reference doc page) | software_practice | Python class that limits OTP requests per phone number |
| C10_rolling_soil_moisture | code | sliding_window_aggregation | agriculture_and_food | Original: a fitness app shows a 7-day rolling average of steps instead of daily counts | original_scenario | Python function for a rolling average of soil-moisture sensor readings with gaps |
| C11_cached_routine_fallback | code | graceful_degradation | web_and_mobile_apps | Software practice: serve stale cached content when the origin fails (for example HTTP stale-if-error, RFC 5861) | software_practice | Python function that returns a class routine, falling back to the last cached copy when the server call fails |
| C12_validate_marks_csv | code | fail_fast_validation | exams_and_assessment | Original: a launch team runs every go/no-go check before fuelling, and stops at the first failed check | original_scenario | Python function that checks an exam-marks CSV before import and reports the first problem |
| C13_memo_points_table | code | result_memoisation | sports_and_recreation | Python docs for functools.lru_cache | software_practice | Python function for an inter-university cricket points table where the same match result lookup repeats |
| C14_tiebreak_room_allotment | code | deterministic_tie_breaking | housing_and_facilities | ICC playing conditions: teams level on points are separated by fixed tie-break rules in order (cite the ICC page) | documented_case | Python function that ranks hall-seat applicants with ties broken by fixed rules |
| C15_canary_meter_firmware | code | staged_rollout | energy_and_utilities | Google SRE book chapter on canarying releases | software_practice | Python function that plans firmware update waves for 5,000 prepaid smart meters |

If a source fact cannot be confirmed, switch the card to an `original_scenario` and say so in `notes`. Do not change the relation family or the target domain without writing why in `notes`.

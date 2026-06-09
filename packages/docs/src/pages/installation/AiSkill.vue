<template>
    <div class="content">
        <h2>What is a Buefy Skill?</h2>
        <p>
            A <strong>Skill</strong> is a structured Markdown reference file that AI coding agents
            load to understand a library's component API without guessing. When an agent has the
            Buefy skill loaded, it can generate accurate component code — correct prop names,
            proper <code>v-model</code> targets, right slot names — instead of hallucinating details
            from outdated training data.
        </p>
        <p>The Buefy skill (<code>SKILL.md</code>) lives at the root of this repository and covers:</p>
        <ul>
            <li>Install and plugin registration patterns</li>
            <li>Core usage rules (type prop, size values, <code>&lt;b-field&gt;</code> wrapper, icons, programmatic APIs)</li>
            <li>All 42 Buefy components with key props, slots, and minimal examples</li>
            <li>Common patterns (login form, data table with server pagination, confirm dialog)</li>
        </ul>
        <p>
            It works with any AI coding agent that supports skill or context files, including
            Claude Code, GitHub Copilot, Cursor, Codex, Windsurf, and Gemini CLI.
        </p>

        <hr>

        <h2>Installing the Skill</h2>

        <h3>Option A — Using the <code>skills</code> CLI</h3>
        <p>
            If your agent supports the
            <a href="https://github.com/anthropics/skills" target="_blank" rel="noopener noreferrer">skills CLI</a>,
            run this in your project root:
        </p>
        <CodeView code="npx skills add buefy/buefy" lang="bash" expanded />

        <h3>Option B — Manual copy</h3>
        <p>
            Download <code>SKILL.md</code> from the
            <a href="https://github.com/buefy/buefy/blob/dev/SKILL.md" target="_blank" rel="noopener noreferrer">Buefy repository</a>
            and place it in your project root. Most agents automatically pick up skill files in the
            project root or a <code>.claude/</code> / <code>.github/</code> subdirectory — check
            your agent's documentation for the exact path.
        </p>

        <h3>Option C — Per-agent setup</h3>
        <p>
            Each agent has its own way to load a context file. Common approaches:
        </p>
        <ul>
            <li>
                <strong>Claude Code</strong> — add a reference in
                <code>CLAUDE.md</code> or place <code>SKILL.md</code> anywhere in the project;
                Claude Code reads project files automatically.
            </li>
            <li>
                <strong>GitHub Copilot</strong> — use a
                <code>.github/copilot-instructions.md</code> file and include the skill content or
                a link to it.
            </li>
            <li>
                <strong>Cursor</strong> — add the skill content to a
                <code>.cursorrules</code> file in your project root.
            </li>
            <li>
                <strong>Windsurf</strong> — add the skill content to a
                <code>.windsurfrules</code> file in your project root.
            </li>
        </ul>

        <hr>

        <h2>Usage</h2>
        <p>
            Once the skill is loaded you can write natural language prompts and the agent will
            generate correct Buefy code. Some example prompts:
        </p>
        <CodeView
            :code="examplePrompts"
            lang="text"
            expanded
        />
        <p>
            The agent will wrap form inputs in <code>&lt;b-field&gt;</code>, use
            <code>type="is-primary"</code> not <code>class="is-primary"</code>, bind
            <code>v-model</code> correctly per component, and follow the other rules documented
            in the skill.
        </p>

        <hr>

        <h2>SKILL.md reference</h2>
        <p>
            The full skill file is available at
            <a href="https://github.com/buefy/buefy/blob/dev/SKILL.md" target="_blank" rel="noopener noreferrer">
                github.com/buefy/buefy/blob/dev/SKILL.md
            </a>.
        </p>
        <p>It is structured as follows:</p>
        <ul>
            <li><strong>Frontmatter</strong> — machine-readable name, description, and version metadata</li>
            <li><strong>When to run</strong> — trigger conditions so the agent activates the skill automatically</li>
            <li><strong>Install</strong> — full bundle and individual component registration examples</li>
            <li><strong>Usage rules</strong> — 8 Buefy-specific rules agents must follow</li>
            <li><strong>Colors &amp; Types</strong> — all valid <code>type</code> and <code>size</code> values</li>
            <li><strong>Components</strong> — one entry per component with props, slots, and a working template example</li>
            <li><strong>Common patterns</strong> — login form, server-side paginated table, confirmation dialog</li>
        </ul>
    </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import CodeView from '@/components/CodeView.vue'

export default defineComponent({
    name: 'AiSkill',
    components: {
        CodeView
    },
    data() {
        return {
            examplePrompts: [
                'Create a login form using Buefy with email and password fields and validation messages.',
                'Add a responsive data table with sorting and server-side pagination using Buefy.',
                'Build a modal confirmation dialog that asks the user before deleting a record.',
                'Create a sidebar navigation with collapsible menu items using b-menu.',
                'Add a multi-step wizard form with b-steps and a progress indicator.'
            ].join('\n')
        }
    }
})
</script>

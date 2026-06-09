<template>
    <div class="content">
        <p>
            <a href="https://github.com/buefy/buefy-mcp" target="_blank" rel="noopener noreferrer">buefy-mcp</a>
            is a lightweight local
            <a href="https://modelcontextprotocol.io" target="_blank" rel="noopener noreferrer">Model Context Protocol (MCP)</a>
            server that exposes the full Buefy 3 component documentation to any MCP-compatible
            AI client — Claude Code, Claude Desktop, Cursor, Cline, Windsurf, and others.
        </p>
        <p>
            Instead of relying on training-data snapshots, the agent queries the MCP server for
            live, accurate prop tables, event names, slot names, and usage examples at
            generation time.
        </p>

        <h2>Available tools</h2>
        <table>
            <thead>
                <tr>
                    <th>Tool</th>
                    <th>Description</th>
                </tr>
            </thead>
            <tbody>
                <tr>
                    <td><code>buefy_list_components</code></td>
                    <td>List all 42 components with one-line descriptions</td>
                </tr>
                <tr>
                    <td><code>buefy_get_component</code></td>
                    <td>Full docs for a component: props, events, slots, methods</td>
                </tr>
                <tr>
                    <td><code>buefy_search</code></td>
                    <td>Search across all component docs by keyword</td>
                </tr>
                <tr>
                    <td><code>buefy_get_installation</code></td>
                    <td>Installation and setup instructions for Buefy</td>
                </tr>
            </tbody>
        </table>

        <hr>

        <h2>Setup</h2>

        <h3>1. Clone and install</h3>
        <CodeView code="git clone https://github.com/buefy/buefy-mcp.git
cd buefy-mcp
npm install" lang="bash" expanded />

        <h3>2. Configure your MCP client</h3>
        <p>Add the server to your client's MCP configuration. Replace <code>/absolute/path/to/buefy-mcp</code> with the actual path on your machine.</p>

        <b-tabs type="is-boxed">
            <b-tab-item label="Claude Code">
                <p>Add to <code>.claude/settings.json</code> in your project:</p>
                <CodeView :code="claudeCodeConfig" lang="json" expanded />
            </b-tab-item>

            <b-tab-item label="Claude Desktop">
                <p>Add to <code>claude_desktop_config.json</code>:</p>
                <CodeView :code="claudeDesktopConfig" lang="json" expanded />
            </b-tab-item>

            <b-tab-item label="npx (after npm publish)">
                <p>Once <code>buefy-mcp</code> is published to npm, no local clone is needed:</p>
                <CodeView :code="npxConfig" lang="json" expanded />
            </b-tab-item>
        </b-tabs>

        <hr>

        <h2>Keeping docs up to date</h2>
        <p>
            The server ships with a bundled snapshot of the Buefy docs. To re-download the
            latest from the <code>dev</code> branch:
        </p>
        <CodeView code="npm run update-data" lang="bash" expanded />

        <hr>

        <h2>Testing</h2>
        <p>You can verify the server works before connecting a client:</p>
        <CodeView :code="testingCommands" lang="bash" expanded />
        <p>Or launch the interactive MCP inspector:</p>
        <CodeView code="npx @modelcontextprotocol/inspector node index.js" lang="bash" expanded />

        <hr>

        <h2>Related</h2>
        <ul>
            <li>
                <router-link to="/documentation/ai-skill">AI &amp; Skills</router-link>
                — Use <code>SKILL.md</code> as a lightweight alternative that requires no server
            </li>
            <li>
                <a href="https://github.com/buefy/buefy-mcp" target="_blank" rel="noopener noreferrer">
                    buefy-mcp on GitHub
                </a>
            </li>
            <li>
                <a href="https://modelcontextprotocol.io" target="_blank" rel="noopener noreferrer">
                    Model Context Protocol documentation
                </a>
            </li>
        </ul>
    </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import { BTabs, BTabItem } from 'buefy'
import CodeView from '@/components/CodeView.vue'

export default defineComponent({
    name: 'BuefyMcp',
    components: {
        BTabs,
        BTabItem,
        CodeView
    },
    data() {
        return {
            claudeCodeConfig: JSON.stringify({
                mcpServers: {
                    buefy: {
                        command: 'node',
                        args: ['/absolute/path/to/buefy-mcp/index.js'],
                        type: 'stdio'
                    }
                }
            }, null, 2),
            claudeDesktopConfig: JSON.stringify({
                mcpServers: {
                    buefy: {
                        command: 'node',
                        args: ['/absolute/path/to/buefy-mcp/index.js']
                    }
                }
            }, null, 2),
            npxConfig: JSON.stringify({
                mcpServers: {
                    buefy: {
                        command: 'npx',
                        args: ['-y', 'buefy-mcp']
                    }
                }
            }, null, 2),
            testingCommands: [
                '# List available tools',
                `echo '{"jsonrpc":"2.0","id":1,"method":"tools/list"}' | node index.js`,
                '',
                '# Get BButton documentation',
                `echo '{"jsonrpc":"2.0","id":2,"method":"tools/call","params":{"name":"buefy_get_component","arguments":{"component_name":"BButton"}}}' | node index.js`
            ].join('\n')
        }
    }
})
</script>

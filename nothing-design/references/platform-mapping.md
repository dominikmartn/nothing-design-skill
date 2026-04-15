# Nothing Design System — Platform Mapping

## 1. HTML / CSS / WEB

Load fonts via Google Fonts `<link>` or `@import`. Use CSS custom properties, `rem` for type, `px` for spacing/borders. Dark/light via `prefers-color-scheme` or class toggle.

```css
:root {
  --black: #000000;
  --surface: #111111;
  --surface-raised: #1A1A1A;
  --border: #222222;
  --border-visible: #333333;
  --text-disabled: #666666;
  --text-secondary: #999999;
  --text-primary: #E8E8E8;
  --text-display: #FFFFFF;
  --accent: #D71921;
  --accent-subtle: rgba(215,25,33,0.15);
  --success: #4A9E5C;
  --warning: #D4A843;
  --interactive: #5B9BF6;
  --space-xs: 4px;
  --space-sm: 8px;
  --space-md: 16px;
  --space-lg: 24px;
  --space-xl: 32px;
  --space-2xl: 48px;
  --space-3xl: 64px;
  --space-4xl: 96px;
}
```

---

## 2. SWIFTUI / iOS

Register fonts in Info.plist, bundle `.ttf` files. Use `@Environment(\.colorScheme)` for mode switching.

```swift
extension Color {
    static let ndBlack = Color(hex: "000000")
    static let ndSurface = Color(hex: "111111")
    static let ndSurfaceRaised = Color(hex: "1A1A1A")
    static let ndBorder = Color(hex: "222222")
    static let ndBorderVisible = Color(hex: "333333")
    static let ndTextDisabled = Color(hex: "666666")
    static let ndTextSecondary = Color(hex: "999999")
    static let ndTextPrimary = Color(hex: "E8E8E8")
    static let ndTextDisplay = Color.white
    static let ndAccent = Color(hex: "D71921")
    static let ndSuccess = Color(hex: "4A9E5C")
    static let ndWarning = Color(hex: "D4A843")
    static let ndInteractive = Color(hex: "5B9BF6")
}
```

Light mode values in tokens.md Dark/Light table. Derive Font extension from font stack table (trivial: `.custom("Doto"/"SpaceGrotesk-Regular"/"SpaceMono-Regular", size:)`).

---

## 3. PAPER (DESIGN TOOL)

Use `get_font_family_info` to verify fonts before writing styles. Direct hex values (no CSS variables). Dark mode as default canvas, light mode as separate artboard.

---

## 4. PHOENIX / LIVEVIEW / HEEx

### 4.1 Font Loading

Load Google Fonts in `lib/app_web/components/layouts/root.html.heex` (the outermost HTML template):

```heex
<!-- root.html.heex, inside <head> -->
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Doto:wght@400;500;600;700&family=Space+Grotesk:wght@300;400;500;700&family=Space+Mono:wght@400;700&display=swap" rel="stylesheet">
```

Alternatively, use `@import` at the top of `app.css` (only if not using Tailwind v4's `@import "tailwindcss"` in the same file — they conflict):

```css
@import url('https://fonts.googleapis.com/css2?family=Doto:wght@400;500;600;700&family=Space+Grotesk:wght@300;400;500;700&family=Space+Mono:wght@400;700&display=swap');
```

### 4.2 Tailwind Config — Nothing Design Tokens

**Tailwind v3** (`tailwind.config.js`):

```js
/** @type {import('tailwindcss').Config} */
export default {
  darkMode: 'class',
  theme: {
    extend: {
      colors: {
        nd: {
          black:    '#000000',
          surface:  '#111111',
          raised:   '#1A1A1A',
          border:   '#222222',
          'border-visible': '#333333',
          'text-disabled':  '#666666',
          'text-secondary': '#999999',
          'text-primary':   '#E8E8E8',
          'text-display':   '#FFFFFF',
          accent:   '#D71921',
          success:  '#4A9E5C',
          warning:  '#D4A843',
          info:     '#999999',
          interactive: '#5B9BF6',
        },
      },
      fontFamily: {
        display:  ['Doto', '"Space Mono"', 'monospace'],
        sans:     ['"Space Grotesk"', '"DM Sans"', 'system-ui', 'sans-serif'],
        mono:     ['"Space Mono"', '"JetBrains Mono"', '"SF Mono"', 'monospace'],
      },
      fontSize: {
        'display-xl':  ['72px', { lineHeight: '1.0',  letterSpacing: '-0.03em' }],
        'display-lg':  ['48px', { lineHeight: '1.05', letterSpacing: '-0.02em' }],
        'display-md':  ['36px', { lineHeight: '1.1',  letterSpacing: '-0.02em' }],
        heading:       ['24px', { lineHeight: '1.2',  letterSpacing: '-0.01em' }],
        subheading:    ['18px', { lineHeight: '1.3' }],
        body:          ['16px', { lineHeight: '1.5' }],
        'body-sm':     ['14px', { lineHeight: '1.5', letterSpacing: '0.01em' }],
        caption:       ['12px', { lineHeight: '1.4', letterSpacing: '0.04em' }],
        label:         ['11px', { lineHeight: '1.2', letterSpacing: '0.08em' }],
      },
      spacing: {
        '2xs': '2px',
        xs:  '4px',
        sm:  '8px',
        md:  '16px',
        lg:  '24px',
        xl:  '32px',
        '2xl': '48px',
        '3xl': '64px',
        '4xl': '96px',
      },
      transitionTimingFunction: {
        'nd-ease': 'cubic-bezier(0.25, 0.1, 0.25, 1)',
      },
      transitionDuration: {
        'nd-micro': '150ms',
        'nd-transition': '300ms',
      },
    },
  },
}
```

**Tailwind v4** (`app.css`):

```css
@import "tailwindcss";

@theme {
  --color-nd-black: #000000;
  --color-nd-surface: #111111;
  --color-nd-raised: #1A1A1A;
  --color-nd-border: #222222;
  --color-nd-border-visible: #333333;
  --color-nd-text-disabled: #666666;
  --color-nd-text-secondary: #999999;
  --color-nd-text-primary: #E8E8E8;
  --color-nd-text-display: #FFFFFF;
  --color-nd-accent: #D71921;
  --color-nd-success: #4A9E5C;
  --color-nd-warning: #D4A843;
  --color-nd-interactive: #5B9BF6;

  --font-display: "Doto", "Space Mono", monospace;
  --font-sans: "Space Grotesk", "DM Sans", system-ui, sans-serif;
  --font-mono: "Space Mono", "JetBrains Mono", "SF Mono", monospace;

  --text-display-xl: 72px;
  --text-display-xl--line-height: 1.0;
  --text-display-xl--letter-spacing: -0.03em;
  --text-display-lg: 48px;
  --text-display-lg--line-height: 1.05;
  --text-display-md: 36px;
  --text-heading: 24px;
  --text-subheading: 18px;
  --text-body: 16px;
  --text-body-sm: 14px;
  --text-caption: 12px;
  --text-label: 11px;

  --spacing-2xs: 2px;
  --spacing-xs: 4px;
  --spacing-sm: 8px;
  --spacing-md: 16px;
  --spacing-lg: 24px;
  --spacing-xl: 32px;
  --spacing-2xl: 48px;
  --spacing-3xl: 64px;
  --spacing-4xl: 96px;

  --transition-timing-function-nd-ease: cubic-bezier(0.25, 0.1, 0.25, 1);
  --transition-duration-nd-micro: 150ms;
  --transition-duration-nd-transition: 300ms;
}
```

### 4.3 Dark / Light Mode in LiveView

Use a `dark` class on the `<html>` or outermost `<div>` in `root.html.heex`. Toggle via `Phoenix.LiveView.JS`:

```heex
<!-- root.html.heex — outer wrapper -->
<div id="app-root" class="dark:bg-nd-black dark:text-nd-text-display bg-[#F5F5F5] text-nd-black">
  <%= @inner_content %>
</div>

<!-- Theme toggle button in a LiveView template -->
<button phx-click={JS.toggle_attribute({"class", "dark", "dark", ""}, to: "#app-root")}>
  <span class="font-mono text-label uppercase">[ THEME ]</span>
</button>
```

Alternative — toggle a `dark` class directly:

```heex
<button phx-click={JS.add_class("dark", to: "html") |> JS.remove_class("dark", to: "html")}>
```

In the LiveView `mount/3`, set initial theme from user preference or session:

```elixir
def mount(_params, %{"theme" => theme} = _session, socket) do
  dark_class = if theme == "dark", do: "dark", else: ""
  {:ok, assign(socket, dark_class: dark_class)}
end
```

Light mode values: background `#F5F5F5`, surface `#FFFFFF`, raised `#F0F0F0`, borders `#E8E8E8` / `#CCCCCC`, text `#000000` / `#1A1A1A` / `#666666` / `#999999`. The Nothing system keeps accent/status colors identical across modes — use Tailwind's `dark:` modifier for surface/text tokens only.

### 4.4 HEEx Component Mappings

**Nothing Design components become Phoenix function components** (`def component(assigns) do ~H"""...""" end`). Stateful or event-heavy sections (dashboards, live data widgets) use `Phoenix.LiveComponent`.

#### Cards / Surfaces

```heex
<.surface class="p-md rounded-lg">
  <:title>Network Speed</:title>
  <:subtitle>Real-time throughput</:subtitle>
  <:body>
    <p class="font-display text-display-lg text-nd-text-display">36<span class="font-mono text-label text-nd-text-secondary">GB/s</span></p>
  </:body>
</.surface>
```

Define as:

```elixir
attr :class, :string, default: nil
slot :title, required: false
slot :subtitle, required: false
slot :body, required: true

def surface(assigns) do
  ~H"""
  <div class={["bg-nd-surface dark:bg-nd-surface border border-nd-border rounded-xl", @class]}>
    <%= if @title != [], do: ~H"""
    <p class="font-mono text-caption uppercase text-nd-text-secondary px-md pt-md pb-2xs"><%= render_slot(@title) %></p>
    """ %>
    <%= if @subtitle != [], do: ~H"""
    <p class="font-sans text-body-sm text-nd-text-secondary px-md pb-xs"><%= render_slot(@subtitle) %></p>
    """ %>
    <div class="px-md pb-md"><%= render_slot(@body) %></div>
  </div>
  """
end
```

#### Buttons

```heex
<.nd_button variant="primary" phx-click="do_action">[ EXECUTE ]</.nd_button>
<.nd_button variant="secondary">[ CANCEL ]</.nd_button>
<.nd_button variant="destructive">[ ABORT ]</.nd_button>
```

```elixir
attr :variant, :string, values: ["primary", "secondary", "ghost", "destructive"], default: "secondary"
attr :rest, :global
slot :inner_block, required: true

def nd_button(assigns) do
  ~H"""
  <button
    class={[
      "font-mono text-label uppercase tracking-wider px-6 py-3 min-h-[44px] transition-colors duration-nd-micro ease-nd-ease",
      case @variant do
        "primary" -> "bg-nd-text-display text-nd-black rounded-full"
        "secondary" -> "bg-transparent border border-nd-border-visible text-nd-text-primary rounded-full"
        "ghost" -> "bg-transparent text-nd-text-secondary"
        "destructive" -> "bg-transparent border border-nd-accent text-nd-accent rounded-full"
      end
    ]}
    {@rest}
  >
    <%= render_slot(@inner_block) %>
  </button>
  """
end
```

#### Inputs

```heex
<.nd_input label="ENDPOINT" type="text" phx-debounce="300" />
```

```elixir
attr :label, :string, required: true
attr :type, :string, default: "text"
attr :rest, :global

def nd_input(assigns) do
  ~H"""
  <div class="mb-md">
    <label class="font-mono text-label uppercase text-nd-text-secondary"><%= @label %></label>
    <input
      type={@type}
      class="w-full bg-transparent font-mono text-body text-nd-text-primary border-b border-nd-border-visible py-xs focus:border-nd-text-primary focus:outline-none transition-colors duration-nd-micro"
      {@rest}
    />
  </div>
  """
end
```

#### Data Rows / Lists

```heex
<.nd_data_row label="STATUS" value="ACTIVE" status="success" />
<.nd_data_row label="LATENCY" value="12" unit="ms" status="warning" />
```

```elixir
attr :label, :string, required: true
attr :value, :string, required: true
attr :unit, :string, default: nil
attr :status, :string, values: ["success", "warning", "error", "neutral"], default: "neutral"

def nd_data_row(assigns) do
  value_color = case assigns[:status] do
    "success" -> "text-nd-success"
    "warning" -> "text-nd-warning"
    "error" -> "text-nd-accent"
    _ -> "text-nd-text-primary"
  end

  assigns = assign(assigns, :value_color, value_color)

  ~H"""
  <div class="flex justify-between items-baseline py-xs border-b border-nd-border">
    <span class="font-mono text-label uppercase text-nd-text-secondary"><%= @label %></span>
    <span class={"font-mono text-body #{assigns.value_color}"}>
      <%= @value %><%= if @unit, do: ~H""" <span class="font-mono text-label text-nd-text-secondary"><%= @unit %></span> """ %>
    </span>
  </div>
  """
end
```

#### Tags / Chips

```heex
<.nd_tag>ACTIVE</.nd_tag>
<.nd_tag variant="active">SYNCING</.nd_tag>
```

```elixir
attr :variant, :string, values: ["default", "active"], default: "default"
slot :inner_block, required: true

def nd_tag(assigns) do
  ~H"""
  <span class={[
    "font-mono text-caption uppercase px-3 py-1 border",
    case @variant do
      "active" -> "border-nd-text-visible text-nd-text-display"
      "default" -> "border-nd-border-visible text-nd-text-secondary"
    end
  ]}>
    <%= render_slot(@inner_block) %>
  </span>
  """
end
```

#### Segmented Progress Bar

```heex
<.nd_progress value={7} total={10} label="STORAGE" readout="70%" />
```

```elixir
attr :value, :integer, required: true
attr :total, :integer, required: true
attr :label, :string, required: true
attr :readout, :string, required: true
attr :status, :string, values: ["neutral", "over", "good", "moderate"], default: "neutral"

def nd_progress(assigns) do
  fill = case assigns[:status] do
    "over" -> "bg-nd-accent"
    "good" -> "bg-nd-success"
    "moderate" -> "bg-nd-warning"
    _ -> "bg-nd-text-display"
  end
  empty = "bg-nd-border dark:bg-nd-border"
  segments = Enum.map(1..assigns.total, fn i -> i <= assigns.value end)
  assigns = assign(assigns, segments: segments, fill: fill, empty: empty)

  ~H"""
  <div>
    <div class="flex justify-between items-baseline mb-xs">
      <span class="font-mono text-label uppercase text-nd-text-secondary"><%= @label %></span>
      <span class="font-mono text-label text-nd-text-primary"><%= @readout %></span>
    </div>
    <div class="flex gap-2px w-full">
      <%= for filled? <- @segments do %>
        <div class={"flex-1 h-3 #{if filled?, do: @fill, else: @empty}"}></div>
      <% end %>
    </div>
  </div>
  """
end
```

#### Toggles / Switches

```heex
<.nd_toggle label="AUTO-SYNC" checked={@auto_sync} phx-click="toggle_auto_sync" />
```

```elixir
attr :label, :string, required: true
attr :checked, :boolean, default: false
attr :rest, :global

def nd_toggle(assigns) do
  ~H"""
  <button
    class="flex items-center gap-sm min-h-[44px]"
    role="switch"
    aria-checked={@checked}
    {@rest}
  >
    <span class="font-mono text-label uppercase text-nd-text-secondary"><%= @label %></span>
    <span class={["relative w-12 h-6 rounded-full border transition-colors duration-nd-micro",
      if(@checked, do: "bg-nd-text-display border-nd-text-display", else: "bg-transparent border-nd-border-visible")]}>
      <span class={["absolute top-0.5 left-0.5 w-5 h-5 rounded-full transition-transform duration-nd-micro",
        if(@checked, do: "translate-x-6 bg-nd-black", else: "bg-nd-text-disabled")]}/>
    </span>
  </button>
  """
end
```

#### Tables / Data Grids

```heex
<table class="w-full">
  <thead>
    <tr class="border-b border-nd-border-visible">
      <th class="font-mono text-label uppercase text-nd-text-secondary px-4 py-3 text-left">Node</th>
      <th class="font-mono text-label uppercase text-nd-text-secondary px-4 py-3 text-right">Throughput</th>
      <th class="font-mono text-label uppercase text-nd-text-secondary px-4 py-3 text-right">Status</th>
    </tr>
  </thead>
  <tbody>
    <%= for node <- @nodes do %>
      <tr class="border-b border-nd-border hover:bg-nd-raised transition-colors">
        <td class="font-sans text-body text-nd-text-primary px-4 py-3"><%= node.name %></td>
        <td class="font-mono text-body text-nd-text-primary px-4 py-3 text-right"><%= node.throughput %></td>
        <td class="font-mono text-caption uppercase px-4 py-3 text-right <%= node.status_color %>"><%= node.status %></td>
      </tr>
    <% end %>
  </tbody>
</table>
```

### 4.5 Slot Composition Patterns

Nothing Design components with variable content use HEEx **named slots** — the HEEx equivalent of React `children`:

```heex
<.surface>
  <:header>
    <.nd_tag>DASHBOARD</.nd_tag>
  </:header>
  <:body>
    <p class="font-display text-display-lg">42</p>
  </:body>
  <:footer>
    <span class="font-mono text-label text-nd-text-disabled">LAST SYNC: 14:32 UTC</span>
  </:footer>
</.surface>
```

Declare slots explicitly:

```elixir
attr :class, :string, default: nil
slot :header, required: false
slot :body, required: true
slot :footer, required: false

def surface(assigns) do
  ~H"""
  <div class={["bg-nd-surface border border-nd-border rounded-xl", @class]}>
    <%= if @header != [], do: ~H"""
    <div class="px-md pt-md"><%= render_slot(@header) %></div>
    """ %>
    <div class="px-md py-md"><%= render_slot(@body) %></div>
    <%= if @footer != [], do: ~H"""
    <div class="px-md pb-md"><%= render_slot(@footer) %></div>
    """ %>
  </div>
  """
end
```

For repeating items (data rows, list items, table rows), pass a list assign and render with `:for`:

```heex
<.nd_list items={@devices} />
```

```elixir
attr :items, :list, required: true

def nd_list(assigns) do
  ~H"""
  <div>
    <%= for item <- @items do %>
      <.nd_data_row label={item.label} value={item.value} unit={item.unit} status={item.status} />
    <% end %>
  </div>
  """
end
```

### 4.6 JS Interactivity — `Phoenix.LiveView.JS` vs Alpine.js

**Default: `Phoenix.LiveView.JS`.** Nothing Design animations are subtle (150–250ms ease-out, opacity over position) — `JS` handles all of them natively without a client-side framework.

```heex
<!-- Toggle visibility -->
<button phx-click={JS.toggle(to: "#details-panel", time: 200, in: {"ease-out duration-200", "opacity-0", "opacity-100"}, out: {"ease-out duration-200", "opacity-100", "opacity-0"})}>
  [ DETAILS ]
</button>

<!-- Add/remove class for theme toggle -->
<button phx-click={JS.add_class("dark", to: "html")}>
  [ DARK ]
</button>

<!-- Chain: hide element, then push event -->
<button phx-click={JS.hide(to: "#toast", time: 200) |> JS.push("dismiss_toast")}>
  [ DISMISS ]
</button>
```

**Use Alpine.js only when:** the project already has Alpine loaded and the interaction is purely client-side with no server state change (e.g., dropdown open/close, tab switching within a static component). Never use Alpine for data mutations — those belong in `handle_event/2` on the LiveView.

### 4.7 LiveComponent Strategy

Use `Phoenix.LiveComponent` (mounted components with `use Phoenix.LiveComponent`) when a UI section has:

- Its own local state that would pollute the parent LiveView's assigns
- Independent `handle_event` callbacks
- Periodic updates via `handle_info` (e.g., a live metric widget)

Pure rendering → function components (`def component(assigns)`). State + events → `LiveComponent`.

```elixir
defmodule AppWeb.Widgets.MetricComponent do
  use Phoenix.LiveComponent

  attr :metric_id, :string, required: true
  attr :label, :string, required: true

  def render(assigns) do
    ~H"""
    <div class="bg-nd-surface border border-nd-border rounded-xl p-md">
      <p class="font-mono text-caption uppercase text-nd-text-secondary"><%= @label %></p>
      <p class="font-display text-display-lg text-nd-text-display"><%= @value %></p>
      <p class="font-mono text-label text-nd-text-disabled"><%= @unit %> · <%= @updated_at %></p>
    </div>
    """
  end
end
```

### 4.8 Layout Strategy

Nothing Design screens in LiveView follow this structure:

```heex
<Layouts.app flash={@flash} current_scope={@current_scope}>
  <div class="min-h-screen bg-nd-black dark:bg-nd-black bg-[#F5F5F5]">
    <.live_nav />
    <main class="px-lg py-xl max-w-3xl mx-auto">
      <%= @inner_content %>
    </main>
  </div>
</Layouts.app>
```

Key rules:

- **No shadows, no blur** — surfaces separate via borders and background contrast only
- **Hero elements breathe** — 64–96px padding around primary content
- **Labels always Space Mono, ALL CAPS** — use `font-mono text-label uppercase`
- **Numbers are Space Mono** — values, metrics, timestamps
- **Active nav item** — `text-nd-text-display` with a dot prefix or underline, inactive items `text-nd-disabled`

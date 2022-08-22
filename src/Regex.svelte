<script>
    let regex = "[A-Z]";
    let text = "A Tale of Two Cities by Charles Dickens";

    $: pattern = createRegex(regex);

    $: result = text.match(pattern);

    // View after matches are found in text.
    $: output = createOutput(text, result, pattern);

    function createRegex(pattern) {
        let regex = "";
        try {
            regex = new RegExp(pattern, "g");
        } catch {}
        return regex;
    }

    function createOutput(text, result, pattern) {
        if (!result) return text;

        const element = (it) =>
            `<div class="tooltip" data-tip="Match: ${it}"><span class="font-mono bg-teal-500 text-white border rounded-sm">${it}</span></div>`;

        return text.replaceAll(pattern, element);
    }
</script>

<header>
    <div class="navbar">
        <a href="/" class="btn btn-ghost text-xl normal-case">
            Regex tester in Svelte
        </a>
    </div>
</header>

<div class="grid gap-4 rounded-lg p-4">
    <input
        type="text"
        placeholder="Regex"
        bind:value={regex}
        class:input-error={!pattern}
        class="input input-bordered w-1/2"
    />

    <div class="badge">{result?.length || 0} matches</div>

    <textarea
        type="text"
        placeholder="Text"
        bind:value={text}
        class="input input-bordered h-36"
    />

    <div class="rounded-lg border border-primary p-4">
        {@html output}
    </div>
</div>

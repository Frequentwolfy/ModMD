# ModMD
Bot for managing groups
const MODMD_MENU = `🤖 ModMD — Command Menu

.menu  — Show this menu
.help  — Get help
.rules — View group rules
.filter — View moderation status
.rps   — Play Rock Paper Scissors

ModMD • Group moderation bot`;

function handleModMDCommand(message) {
  const command = message.trim().toLowerCase();

  switch (command) {
    case ". menu":
    case ".menu":
      return MODMD_MENU;

    case ".help":
      return "Need help? Send .menu to see all commands.";

    case ".rules":
      return "📜 Group rules\n1. Be respectful.\n2. Avoid blocked words.\n3. Follow the group admins' instructions.";

    case ".filter":
      return "🛡️ ModMD word filtering is configured in the dashboard. Live status requires a connected bot.";

    case ".rps":
      return "✂️ Rock Paper Scissors!\nChoose: .rps rock, .rps paper, or .rps scissors";

    default:
      if (command.startsWith(".rps ")) {
        const choice = command.slice(5).trim();
        if (!["rock", "paper", "scissors"].includes(choice)) {
          return "Choose .rps rock, .rps paper, or .rps scissors";
        }

        const moves = ["rock", "paper", "scissors"];
        const bot = moves[Math.floor(Math.random() * moves.length)];

        if (choice === bot) return `Draw! You both chose ${bot}.`;

        const wins =
          (choice === "rock" && bot === "scissors") ||
          (choice === "paper" && bot === "rock") ||
          (choice === "scissors" && bot === "paper");

        return wins
          ? `🎉 You win! ModMD chose ${bot}.`
          : `ModMD wins! It chose ${bot}.`;
      }

      return null;
  }
}

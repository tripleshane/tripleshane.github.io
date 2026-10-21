# Welcome to My Portfolio Hello! My name is tripleshane .
## About Me
Click here to learn more → [About Me](about.md)
## Notebook
Click here to go to my notebook → [Notebook](notebook.md)
## Projects
- Project 1: Minecraft Coding?
  "what I have"([
    {
        "seesky": true,
        "mintime": 0,
        "maxtime": 12000,
        "hostile": true,
        "result": "deny"
    }
])
- Project 2: HUNTERS(VIBE CODED)- {import javax.swing.*;

import java.awt.*;

import java.awt.event.*;

import java.util.ArrayList;

import java.util.Iterator;

import java.util.List;

import java.util.Random;

public class LearningHunter extends JPanel implements ActionListener, KeyListener {

    private static final int WIDTH = 1100;

    private static final int HEIGHT = 750;

    private static final int BORDER = 25;

    private static final int PLAYER_SIZE = 24;

    private static final int HUNTER_SIZE = 28;

    private static final double PLAYER_SPEED = 250;

    private static final double PLAYER_DASH_SPEED = 900;

    private static final double PLAYER_DASH_DURATION = 0.18;

    private static final double PLAYER_DASH_COOLDOWN = 1.2;

    private static final double HUNTER_START_SPEED = 195;

    private static final double HUNTER_MAX_SPEED = 240;

    private static final double HUNTER_ACCELERATION = 24;

    private static final double HUNTER_DASH_SPEED = 900;

    private static final double HUNTER_LAUNCH_SPEED = 1200;

    private static final double HUNTER_DASH_DURATION = 0.20;

    private static final double HUNTER_DASH_COOLDOWN = 1.7;

    private static final double HUNTER_RESPAWN_DELAY = 15.0;

    private static final double ROUND_LENGTH = 30.0;
    private static final int ITEM_PRICE = 100;
    private static final double HUNTER_NEARBY_RADIUS = 130.0;
    private static final double DASH_REFRESH_COOLDOWN = 2.0;

    private final Timer timer = new Timer(16, this);

    private final Random random = new Random();

    private final boolean[] keys = new boolean[256];

    private double playerX = 80;

    private double playerY = 80;

    private double playerVX;

    private double playerVY;

    private double playerDashTime;

    private double playerDashCooldown;

    private double playerStunTime;

    private double playerWallJumpTime;
    private double playerWallJumpStartX, playerWallJumpStartY, playerWallJumpTargetX, playerWallJumpTargetY;

    private double playerDashDirX;

    private double playerDashDirY;

    private double playerOverdriveTime;

    private boolean shieldActive;

    private boolean playerInvulnerable;

    private double invulnerabilityTime;

    private double hunter1X = 950;

    private double hunter1Y = 100;

    private double hunter1VX;

    private double hunter1VY;

    private double hunter1Speed = HUNTER_START_SPEED;

    private double hunter1DashTime;

    private double hunter1DashCooldown;

    private double hunter1TimeSinceDash = 5.0;

    private double hunter1StunTime;

    private double hunter1WallJumpTime;
    private double hunter1WallJumpStartX, hunter1WallJumpStartY, hunter1WallJumpTargetX, hunter1WallJumpTargetY;

    private double hunter1DashDirX;

    private double hunter1DashDirY;

    private double hunter1RespawnTimer;

    private boolean hunter1Alive = true;
    private boolean huntersRegrouping = false;

    // Stuck detection and escape state for Hunter 1.
    private double hunter1StuckTime;
    private double hunter1StuckAnchorX = hunter1X;
    private double hunter1StuckAnchorY = hunter1Y;
    private double hunter1EscapeTime;
    private double hunter1EscapeTargetX;
    private double hunter1EscapeTargetY;

    private double hunter2X = 950;

    private double hunter2Y = 600;

    private double hunter2VX;

    private double hunter2VY;

    private double hunter2Speed = HUNTER_START_SPEED;

    private double hunter2DashTime;

    private double hunter2DashCooldown;

    private double hunter2TimeSinceDash = 5.0;

    private double hunter2StunTime;

    private double hunter2WallJumpTime;
    private double hunter2WallJumpStartX, hunter2WallJumpStartY, hunter2WallJumpTargetX, hunter2WallJumpTargetY;

    private double hunter2DashDirX;

    private double hunter2DashDirY;

    private double hunter2RespawnTimer;

    private boolean hunter2Alive = true;

    // Stuck detection and escape state for Hunter 2.
    private double hunter2StuckTime;
    private double hunter2StuckAnchorX = hunter2X;
    private double hunter2StuckAnchorY = hunter2Y;
    private double hunter2EscapeTime;
    private double hunter2EscapeTargetX;
    private double hunter2EscapeTargetY;

    private double survivalTime;

    private double bestTime;

    private double roundTimer = ROUND_LENGTH;
    private int cash;
    private double nearbyCashAccumulator;
    private double dashRefreshTimer;
    private int roundsCompleted;
    private enum GamePhase { PLAYING, SHOP, UPGRADE }
    private GamePhase phase = GamePhase.PLAYING;
    private boolean extraChanceUpgrade;
    private boolean extraChanceAvailable;
    private boolean extraChanceUsed;
    private boolean gluedShoes;
    private boolean dashOnDash;
    private boolean dashHitHunterThisDash;
    private boolean marioJump;
    private boolean roomOfMirrors;
    private int[] currentUpgradeChoices = {1, 2, 3};
    private final Rectangle[] mirrors = {
        new Rectangle(WIDTH / 2 - 18, BORDER + 45, 36, 12),
        new Rectangle(WIDTH / 2 - 18, HEIGHT - BORDER - 57, 36, 12),
        new Rectangle(BORDER + 45, HEIGHT / 2 - 18, 12, 36),
        new Rectangle(WIDTH - BORDER - 57, HEIGHT / 2 - 18, 12, 36)
    };

    private boolean dashPressed;

    private boolean useItemPressed;

    private boolean gameOver;

    private ItemType heldItem = null;

    private final List<Snare> snares = new ArrayList<>();

    private String message = "";

    private double messageTimer;

    private enum ItemType {

        SHIELD,

        SHOCKWAVE,

        SNARE_MINE,

        OVERDRIVE,

        PHASE_SHIFT

    }

    private static class Snare {

        double x;

        double y;

        double age;

        Snare(double x, double y) {

            this.x = x;

            this.y = y;

        }

    }

    private final Rectangle[] walls = {

        new Rectangle(260, 130, 35, 230),

        new Rectangle(450, 280, 230, 35),

        new Rectangle(790, 120, 35, 230),

        new Rectangle(170, 480, 250, 35),

        new Rectangle(570, 500, 35, 150),

        new Rectangle(820, 460, 180, 35)

    };

    public LearningHunter() {

        setPreferredSize(new Dimension(WIDTH, HEIGHT));

        setBackground(new Color(25, 25, 32));

        setFocusable(true);

        addKeyListener(this);

        timer.start();

    }

    @Override

    public void actionPerformed(ActionEvent e) {

        double dt = 0.016;

        if (!gameOver) {

            messageTimer = Math.max(0, messageTimer - dt);
            if (phase == GamePhase.PLAYING) {
                survivalTime += dt;
                roundTimer -= dt;
                dashRefreshTimer = Math.max(0, dashRefreshTimer - dt);
                updateNearbyCash(dt);
                if (roundTimer <= 0) endRound();
            }
            if (phase != GamePhase.PLAYING) {
                repaint();
                return;
            }

            playerOverdriveTime = Math.max(0, playerOverdriveTime - dt);

            invulnerabilityTime = Math.max(0, invulnerabilityTime - dt);

            if (invulnerabilityTime <= 0) {

                playerInvulnerable = false;

            }

            updateWallJumpAnimations(dt);
            updatePlayer(dt);

            updateHunters(dt);


            updateSnares(dt);

            checkPlayerCollision();

        }

        repaint();

    }

    // ---------------- PLAYER ----------------

    private void updatePlayer(double dt) {

        playerDashCooldown = Math.max(0, playerDashCooldown - dt);

        playerDashTime = Math.max(0, playerDashTime - dt);

        playerStunTime = Math.max(0, playerStunTime - dt);



        if (useItemPressed) {

            useItem();

            useItemPressed = false;

        }

        if (playerStunTime > 0 || playerWallJumpTime > 0) {

            dashPressed = false;

            playerVX = 0;
            playerVY = 0;
            return;

        }

        double dx = 0;

        double dy = 0;

        if (keys[KeyEvent.VK_W] || keys[KeyEvent.VK_UP]) dy--;

        if (keys[KeyEvent.VK_S] || keys[KeyEvent.VK_DOWN]) dy++;

        if (keys[KeyEvent.VK_A] || keys[KeyEvent.VK_LEFT]) dx--;

        if (keys[KeyEvent.VK_D] || keys[KeyEvent.VK_RIGHT]) dx++;

        double length = Math.sqrt(dx * dx + dy * dy);

        if (length > 0) {

            dx /= length;

            dy /= length;

        }

        if (dashPressed && playerDashCooldown <= 0 && length > 0) {

            playerDashDirX = dx;

            playerDashDirY = dy;

            playerDashTime = PLAYER_DASH_DURATION;

            playerDashCooldown = PLAYER_DASH_COOLDOWN;

        }

        dashPressed = false;

        double normalSpeed = PLAYER_SPEED;

        if (playerOverdriveTime > 0) {

            normalSpeed *= 1.65;

        }

        double dashSpeed = PLAYER_DASH_SPEED;

        if (playerOverdriveTime > 0) {

            dashSpeed *= 1.4;

        }

        if (playerDashTime > 0) {

            playerVX = playerDashDirX * dashSpeed;

            playerVY = playerDashDirY * dashSpeed;

        } else {

            playerVX = dx * normalSpeed;

            playerVY = dy * normalSpeed;

        }

        movePlayer(playerVX * dt, playerVY * dt);

    }

    private void movePlayer(double dx, double dy) {
        boolean dashing = playerDashTime > 0;
        double nextX = playerX + dx;
        double nextY = playerY + dy;

        if (hitsArenaBoundary(nextX, playerY, PLAYER_SIZE)) {
            playerVX = 0;
            if (dashing) {
                playerDashTime = 0; playerStunTime = 2.0;
                showMessage("You dashed into the arena boundary!");
            }
        } else if (hitsInternalWall(nextX, playerY, PLAYER_SIZE)) {
            if (dashing && tryPlayerWallJump()) return;
            playerVX = 0;
            if (dashing) { playerDashTime = 0; playerStunTime = 2.0; }
        } else {
            playerX = nextX;
        }

        nextY = playerY + dy;
        if (hitsArenaBoundary(playerX, nextY, PLAYER_SIZE)) {
            playerVY = 0;
            if (dashing) {
                playerDashTime = 0; playerStunTime = 2.0;
                showMessage("You dashed into the arena boundary!");
            }
        } else if (hitsInternalWall(playerX, nextY, PLAYER_SIZE)) {
            if (dashing && tryPlayerWallJump()) return;
            playerVY = 0;
            if (dashing) { playerDashTime = 0; playerStunTime = 2.0; }
        } else {
            playerY = nextY;
        }

        // Dashing through a mirror teleports to a different mirror, never the same one.
        if (dashing && roomOfMirrors) {
            Rectangle playerRect = new Rectangle((int) playerX, (int) playerY, PLAYER_SIZE, PLAYER_SIZE);
            int enteredMirror = -1;
            for (int i = 0; i < mirrors.length; i++) {
                if (playerRect.intersects(mirrors[i])) {
                    enteredMirror = i;
                    break;
                }
            }
            if (enteredMirror >= 0 && mirrors.length > 1) {
                int destination;
                do {
                    destination = random.nextInt(mirrors.length);
                } while (destination == enteredMirror);

                Rectangle target = mirrors[destination];
                if (destination == 0) { // top mirror: appear just inside the arena
                    playerX = target.getCenterX() - PLAYER_SIZE / 2.0;
                    playerY = target.y + target.height + 5;
                } else if (destination == 1) { // bottom mirror
                    playerX = target.getCenterX() - PLAYER_SIZE / 2.0;
                    playerY = target.y - PLAYER_SIZE - 5;
                } else if (destination == 2) { // left mirror
                    playerX = target.x + target.width + 5;
                    playerY = target.getCenterY() - PLAYER_SIZE / 2.0;
                } else { // right mirror
                    playerX = target.x - PLAYER_SIZE - 5;
                    playerY = target.getCenterY() - PLAYER_SIZE / 2.0;
                }
                playerX = Math.max(BORDER + 2, Math.min(WIDTH - BORDER - PLAYER_SIZE - 2, playerX));
                playerY = Math.max(BORDER + 2, Math.min(HEIGHT - BORDER - PLAYER_SIZE - 2, playerY));
                showMessage("Mirror jump!");
            }
        }
    }

    // ---------------- USING ITEMS ----------------

    private void useItem() {

        if (heldItem == null) {

            showMessage("You aren't holding an item!");

            return;

        }

        switch (heldItem) {

            case SHIELD:

                shieldActive = true;

                showMessage("Impact Shield activated!");

                break;

            case SHOCKWAVE:

                useShockwave();

                showMessage("Shockwave released!");

                break;

            case SNARE_MINE:

                snares.add(new Snare(

                    playerX + PLAYER_SIZE / 2.0,

                    playerY + PLAYER_SIZE / 2.0

                ));

                showMessage("Snare Mine placed!");

                break;

            case OVERDRIVE:

                playerOverdriveTime = 8.0;

                showMessage("Overdrive: speed increased for 8 seconds!");

                break;

            case PHASE_SHIFT:

                if (teleportPlayer()) {

                    showMessage("Phase Shift successful!");

                } else {

                    showMessage("No safe teleport location found!");

                    return;

                }

                break;

        }

        heldItem = null;

    }

    private void useShockwave() {

        double px = playerX + PLAYER_SIZE / 2.0;

        double py = playerY + PLAYER_SIZE / 2.0;

        double radius = 190;

        if (hunter1Alive) {

            double hx = hunter1X + HUNTER_SIZE / 2.0;

            double hy = hunter1Y + HUNTER_SIZE / 2.0;

            if (distance(px, py, hx, hy) <= radius) {

                launchHunterAway(1, px, py, 1.0);

            }

        }

        if (hunter2Alive) {

            double hx = hunter2X + HUNTER_SIZE / 2.0;

            double hy = hunter2Y + HUNTER_SIZE / 2.0;

            if (distance(px, py, hx, hy) <= radius) {

                launchHunterAway(2, px, py, 1.0);

            }

        }

    }

    private boolean teleportPlayer() {

        for (int attempt = 0; attempt < 150; attempt++) {

            double x = BORDER + 20

                + random.nextInt(WIDTH - 2 * BORDER - PLAYER_SIZE - 40);

            double y = BORDER + 20

                + random.nextInt(HEIGHT - 2 * BORDER - PLAYER_SIZE - 40);

            if (hitsWall(x, y, PLAYER_SIZE)) continue;

            if (distance(x, y, hunter1X, hunter1Y) < 170) continue;

            if (distance(x, y, hunter2X, hunter2Y) < 170) continue;

            playerX = x;

            playerY = y;

            playerDashTime = 0;

            playerVX = 0;

            playerVY = 0;

            playerInvulnerable = true;

            invulnerabilityTime = 1.0;

            return true;

        }

        return false;

    }

    private void updateSnares(double dt) {

        Iterator<Snare> iterator = snares.iterator();

        while (iterator.hasNext()) {

            Snare snare = iterator.next();

            snare.age += dt;

            if (snare.age > 20) {

                iterator.remove();

                continue;

            }

            Rectangle trap = new Rectangle(

                (int) snare.x - 12,

                (int) snare.y - 12,

                24, 24

            );

            if (hunter1Alive && trap.intersects(new Rectangle(

                    (int) hunter1X, (int) hunter1Y,

                    HUNTER_SIZE, HUNTER_SIZE))) {

                eliminateHunter(1);

                iterator.remove();

                continue;

            }

            if (hunter2Alive && trap.intersects(new Rectangle(

                    (int) hunter2X, (int) hunter2Y,

                    HUNTER_SIZE, HUNTER_SIZE))) {

                eliminateHunter(2);

                iterator.remove();

            }

        }

    }

    // ---------------- HUNTER AI ----------------

    private void updateHunters(double dt) {

        updateRespawnTimers(dt);

        if (hunter1Alive) {

            hunter1DashCooldown = Math.max(0, hunter1DashCooldown - dt);
            hunter1TimeSinceDash += dt;

            hunter1DashTime = Math.max(0, hunter1DashTime - dt);

            hunter1StunTime = Math.max(0, hunter1StunTime - dt);


            hunter1Speed = Math.min(

                HUNTER_MAX_SPEED,

                hunter1Speed + HUNTER_ACCELERATION * (gluedShoes ? 0.35 : 1.0) * dt

            );

        }

        if (hunter2Alive) {

            hunter2DashCooldown = Math.max(0, hunter2DashCooldown - dt);
            hunter2TimeSinceDash += dt;

            hunter2DashTime = Math.max(0, hunter2DashTime - dt);

            hunter2StunTime = Math.max(0, hunter2StunTime - dt);


            hunter2Speed = Math.min(

                HUNTER_MAX_SPEED,

                hunter2Speed + HUNTER_ACCELERATION * (gluedShoes ? 0.35 : 1.0) * dt

            );

        }

        double px = playerX + PLAYER_SIZE / 2.0;

        double py = playerY + PLAYER_SIZE / 2.0;

        double h1x = hunter1X + HUNTER_SIZE / 2.0;

        double h1y = hunter1Y + HUNTER_SIZE / 2.0;

        double h2x = hunter2X + HUNTER_SIZE / 2.0;

        double h2y = hunter2Y + HUNTER_SIZE / 2.0;

        // Dash at each other either after five seconds without dashing,
        // or immediately whenever they are far enough apart to regroup.
        boolean farApartForRegroup = hunter1Alive && hunter2Alive
                && distance(h1x, h1y, h2x, h2y) > 300;
        boolean bothHaveWaitedToDash = hunter1TimeSinceDash >= 5.0
                && hunter2TimeSinceDash >= 5.0;
        if (hunter1Alive && hunter2Alive
                && (farApartForRegroup || bothHaveWaitedToDash)
                && hunter1DashCooldown <= 0 && hunter2DashCooldown <= 0
                && hunter1DashTime <= 0 && hunter2DashTime <= 0
                && hunter1StunTime <= 0 && hunter2StunTime <= 0
                && hunter1WallJumpTime <= 0 && hunter2WallJumpTime <= 0
                && hunter1EscapeTime <= 0 && hunter2EscapeTime <= 0) {
            // Mutual hunter dashes ignore the usual wall-clearance check.
            tryStartHunterDashOneAtOther(h1x, h1y, h2x, h2y);
            tryStartHunterDashTwoAtOther(h2x, h2y, h1x, h1y);
        }

        double target1X = px;

        double target1Y = py;

        double target2X = px;

        double target2Y = py;

        // If the hunters become moderately separated, prioritize regrouping.
        // Pathfinding guides them toward each other around ordinary walls.
        huntersRegrouping = hunter1Alive && hunter2Alive
                && distance(h1x, h1y, h2x, h2y) > 300;

        if (huntersRegrouping) {
            target1X = h2x;
            target1Y = h2y;
            target2X = h1x;
            target2Y = h1y;
        }

        if (hunter1Alive && hunter2Alive && !huntersRegrouping) {

            double awayX = px - h1x;

            double awayY = py - h1y;

            double len = Math.sqrt(awayX * awayX + awayY * awayY);

            if (len > 0) {

                awayX /= len;

                awayY /= len;

            }

            target2X = px + awayX * 140;

            target2Y = py + awayY * 140;

            if (distance(h1x, h1y, h2x, h2y) < 190) {

                if (distance(h1x, h1y, px, py)

                        < distance(h2x, h2y, px, py)) {

                    target2X = h1x;

                    target2Y = h1y;

                } else {

                    target1X = h2x;

                    target1Y = h2y;

                }

            }

        }

        if (hunter1Alive) {

            updateHunterOne(dt, target1X, target1Y, px, py);

        }

        if (hunter2Alive) {

            updateHunterTwo(dt, target2X, target2Y, px, py);

        }

        checkHunterLaunch();

    }

    /**
     * Detects hunters that have barely moved for 10 seconds. Each hunter gets
     * its own timer and, when triggered, temporarily heads for a safe open
     * position instead of continuing to pursue the player.
     */
    private void updateHunterStuckDetection(double dt) {
        if (hunter1Alive) {
            hunter1EscapeTime = Math.max(0, hunter1EscapeTime - dt);

            if (distance(hunter1X, hunter1Y,
                    hunter1StuckAnchorX, hunter1StuckAnchorY) >= 45) {
                hunter1StuckAnchorX = hunter1X;
                hunter1StuckAnchorY = hunter1Y;
                hunter1StuckTime = 0;
            } else {
                hunter1StuckTime += dt;
            }

            if (hunter1StuckTime >= 10.0 && hunter1EscapeTime <= 0) {
                startHunterEscape(1);
            }
        }

        if (hunter2Alive) {
            hunter2EscapeTime = Math.max(0, hunter2EscapeTime - dt);

            if (distance(hunter2X, hunter2Y,
                    hunter2StuckAnchorX, hunter2StuckAnchorY) >= 45) {
                hunter2StuckAnchorX = hunter2X;
                hunter2StuckAnchorY = hunter2Y;
                hunter2StuckTime = 0;
            } else {
                hunter2StuckTime += dt;
            }

            if (hunter2StuckTime >= 10.0 && hunter2EscapeTime <= 0) {
                startHunterEscape(2);
            }
        }
    }

    private void startHunterEscape(int hunter) {
        double[] target = findEscapeTarget(hunter);

        if (hunter == 1) {
            hunter1EscapeTargetX = target[0] + HUNTER_SIZE / 2.0;
            hunter1EscapeTargetY = target[1] + HUNTER_SIZE / 2.0;
            hunter1EscapeTime = 3.5;
            hunter1StuckTime = 0;
            hunter1StuckAnchorX = hunter1X;
            hunter1StuckAnchorY = hunter1Y;
        } else {
            hunter2EscapeTargetX = target[0] + HUNTER_SIZE / 2.0;
            hunter2EscapeTargetY = target[1] + HUNTER_SIZE / 2.0;
            hunter2EscapeTime = 3.5;
            hunter2StuckTime = 0;
            hunter2StuckAnchorX = hunter2X;
            hunter2StuckAnchorY = hunter2Y;
        }
    }

    private double[] findEscapeTarget(int hunter) {
        double currentX = hunter == 1 ? hunter1X : hunter2X;
        double currentY = hunter == 1 ? hunter1Y : hunter2Y;

        // Prefer a clear location well away from the hunter's current spot.
        for (int attempt = 0; attempt < 160; attempt++) {
            double x = BORDER + 15
                    + random.nextInt(WIDTH - 2 * BORDER - HUNTER_SIZE - 30);
            double y = BORDER + 15
                    + random.nextInt(HEIGHT - 2 * BORDER - HUNTER_SIZE - 30);

            if (hitsWall(x, y, HUNTER_SIZE)) continue;
            if (distance(x, y, currentX, currentY) < 150) continue;

            return new double[] {x, y};
        }

        // Fallback: choose the clearest legal direction from the current spot.
        double cx = currentX + HUNTER_SIZE / 2.0;
        double cy = currentY + HUNTER_SIZE / 2.0;
        double[] direction = findPath(cx, cy, WIDTH / 2.0, HEIGHT / 2.0,
                HUNTER_SIZE);

        double x = currentX + direction[0] * 160;
        double y = currentY + direction[1] * 160;

        if (hitsWall(x, y, HUNTER_SIZE)) {
            return findSafeSpawn(HUNTER_SIZE);
        }

        return new double[] {x, y};
    }

    private void updateHunterOne(

        double dt, double targetX, double targetY,

        double px, double py

    ) {

        if (hunter1StunTime > 0) return;

        double cx = hunter1X + HUNTER_SIZE / 2.0;

        double cy = hunter1Y + HUNTER_SIZE / 2.0;

        double[] direction = findPath(

            cx, cy, targetX, targetY, HUNTER_SIZE

        );

        double dx = direction[0];

        double dy = direction[1];

        double length = Math.sqrt(dx * dx + dy * dy);

        if (length > 0) {

            dx /= length;

            dy /= length;

        }

        boolean seesPlayer = hasLineOfSight(cx, cy, px, py);

        double playerDistance = distance(cx, cy, px, py);

        boolean seesTeammate = hunter2Alive && hasLineOfSight(

            cx, cy,

            hunter2X + HUNTER_SIZE / 2.0,

            hunter2Y + HUNTER_SIZE / 2.0

        );

        boolean launchSetup = hunter2Alive &&

            distance(cx, cy,

                hunter2X + HUNTER_SIZE / 2.0,

                hunter2Y + HUNTER_SIZE / 2.0) < 190;

        if (!huntersRegrouping && hunter1EscapeTime <= 0 &&
                hunter1DashCooldown <= 0 && hunter1DashTime <= 0) {

            if (seesPlayer && playerDistance > 100) {

                tryStartHunterDashOne(cx, cy, px, py);

            } else if (launchSetup && seesTeammate) {

                tryStartHunterDashOne(

                    cx, cy,

                    hunter2X + HUNTER_SIZE / 2.0,

                    hunter2Y + HUNTER_SIZE / 2.0

                );

            }

        }

        if (hunter1DashTime > 0) {

            hunter1VX = hunter1DashDirX * HUNTER_DASH_SPEED;

            hunter1VY = hunter1DashDirY * HUNTER_DASH_SPEED;

        } else {

            hunter1VX = dx * hunter1Speed;

            hunter1VY = dy * hunter1Speed;

        }

        moveHunterOne(hunter1VX * dt, hunter1VY * dt);

    }

    private void updateHunterTwo(

        double dt, double targetX, double targetY,

        double px, double py

    ) {

        if (hunter2StunTime > 0) return;

        double cx = hunter2X + HUNTER_SIZE / 2.0;

        double cy = hunter2Y + HUNTER_SIZE / 2.0;

        double[] direction = findPath(

            cx, cy, targetX, targetY, HUNTER_SIZE

        );

        double dx = direction[0];

        double dy = direction[1];

        double length = Math.sqrt(dx * dx + dy * dy);

        if (length > 0) {

            dx /= length;

            dy /= length;

        }

        boolean seesPlayer = hasLineOfSight(cx, cy, px, py);

        double playerDistance = distance(cx, cy, px, py);

        boolean seesTeammate = hunter1Alive && hasLineOfSight(

            cx, cy,

            hunter1X + HUNTER_SIZE / 2.0,

            hunter1Y + HUNTER_SIZE / 2.0

        );

        boolean launchSetup = hunter1Alive &&

            distance(cx, cy,

                hunter1X + HUNTER_SIZE / 2.0,

                hunter1Y + HUNTER_SIZE / 2.0) < 190;

        if (!huntersRegrouping && hunter2EscapeTime <= 0 &&
                hunter2DashCooldown <= 0 && hunter2DashTime <= 0) {

            if (seesPlayer && playerDistance > 100) {

                tryStartHunterDashTwo(cx, cy, px, py);

            } else if (launchSetup && seesTeammate) {

                tryStartHunterDashTwo(

                    cx, cy,

                    hunter1X + HUNTER_SIZE / 2.0,

                    hunter1Y + HUNTER_SIZE / 2.0

                );

            }

        }

        if (hunter2DashTime > 0) {

            hunter2VX = hunter2DashDirX * HUNTER_DASH_SPEED;

            hunter2VY = hunter2DashDirY * HUNTER_DASH_SPEED;

        } else {

            hunter2VX = dx * hunter2Speed;

            hunter2VY = dy * hunter2Speed;

        }

        moveHunterTwo(hunter2VX * dt, hunter2VY * dt);

    }

    private void tryStartHunterDashOneAtOther(
        double cx, double cy, double tx, double ty
    ) {
        double dx = tx - cx;
        double dy = ty - cy;
        double len = Math.sqrt(dx * dx + dy * dy);
        if (len == 0) return;
        hunter1DashDirX = dx / len;
        hunter1DashDirY = dy / len;
        hunter1DashTime = HUNTER_DASH_DURATION;
        hunter1DashCooldown = HUNTER_DASH_COOLDOWN;
        hunter1TimeSinceDash = 0;
    }

    private void tryStartHunterDashTwoAtOther(
        double cx, double cy, double tx, double ty
    ) {
        double dx = tx - cx;
        double dy = ty - cy;
        double len = Math.sqrt(dx * dx + dy * dy);
        if (len == 0) return;
        hunter2DashDirX = dx / len;
        hunter2DashDirY = dy / len;
        hunter2DashTime = HUNTER_DASH_DURATION;
        hunter2DashCooldown = HUNTER_DASH_COOLDOWN;
        hunter2TimeSinceDash = 0;
    }

    private void tryStartHunterDashOne(

        double cx, double cy, double tx, double ty

    ) {

        double dx = tx - cx;

        double dy = ty - cy;

        double len = Math.sqrt(dx * dx + dy * dy);

        if (len == 0) return;

        dx /= len;

        dy /= len;

        double dashDistance = HUNTER_DASH_SPEED

            * HUNTER_DASH_DURATION;

        if (!isDashPathClear(

            hunter1X, hunter1Y, dx, dy,

            HUNTER_SIZE, dashDistance)) return;

        hunter1DashDirX = dx;

        hunter1DashDirY = dy;

        hunter1DashTime = HUNTER_DASH_DURATION;

        hunter1DashCooldown = HUNTER_DASH_COOLDOWN;
        hunter1TimeSinceDash = 0;

    }

    private void tryStartHunterDashTwo(

        double cx, double cy, double tx, double ty

    ) {

        double dx = tx - cx;

        double dy = ty - cy;

        double len = Math.sqrt(dx * dx + dy * dy);

        if (len == 0) return;

        dx /= len;

        dy /= len;

        double dashDistance = HUNTER_DASH_SPEED

            * HUNTER_DASH_DURATION;

        if (!isDashPathClear(

            hunter2X, hunter2Y, dx, dy,

            HUNTER_SIZE, dashDistance)) return;

        hunter2DashDirX = dx;

        hunter2DashDirY = dy;

        hunter2DashTime = HUNTER_DASH_DURATION;

        hunter2DashCooldown = HUNTER_DASH_COOLDOWN;
        hunter2TimeSinceDash = 0;

    }

    // ---------------- HUNTER LAUNCHES ----------------

    private void checkHunterLaunch() {

        if (!hunter1Alive || !hunter2Alive) return;

        Rectangle h1 = new Rectangle(

            (int) hunter1X, (int) hunter1Y,

            HUNTER_SIZE, HUNTER_SIZE

        );

        Rectangle h2 = new Rectangle(

            (int) hunter2X, (int) hunter2Y,

            HUNTER_SIZE, HUNTER_SIZE

        );

        if (!h1.intersects(h2)) return;

        boolean d1 = hunter1DashTime > 0;

        boolean d2 = hunter2DashTime > 0;

        if (!d1 && !d2) return;

        double dx = hunter2X - hunter1X;

        double dy = hunter2Y - hunter1Y;

        double len = Math.sqrt(dx * dx + dy * dy);

        if (len == 0) {

            dx = 1;

            dy = 0;

            len = 1;

        }

        dx /= len;

        dy /= len;

        if (d1 && d2) {

            hunter1VX = -dx * HUNTER_LAUNCH_SPEED;

            hunter1VY = -dy * HUNTER_LAUNCH_SPEED;

            hunter2VX = dx * HUNTER_LAUNCH_SPEED;

            hunter2VY = dy * HUNTER_LAUNCH_SPEED;

            setHunterDashDirection(1, -dx, -dy);

            setHunterDashDirection(2, dx, dy);

            hunter1DashTime = 0.12;

            hunter2DashTime = 0.12;

        } else if (d1) {

            hunter2VX = dx * HUNTER_LAUNCH_SPEED;

            hunter2VY = dy * HUNTER_LAUNCH_SPEED;

            setHunterDashDirection(2, dx, dy);

            hunter2DashTime = 0.22;

            hunter1VX = -dx * 300;

            hunter1VY = -dy * 300;

        } else {

            hunter1VX = -dx * HUNTER_LAUNCH_SPEED;

            hunter1VY = -dy * HUNTER_LAUNCH_SPEED;

            setHunterDashDirection(1, -dx, -dy);

            hunter1DashTime = 0.22;

            hunter2VX = dx * 300;

            hunter2VY = dy * 300;

        }

        hunter1DashCooldown = Math.max(hunter1DashCooldown, 0.6);

        hunter2DashCooldown = Math.max(hunter2DashCooldown, 0.6);

        hunter1X -= dx * 5;

        hunter1Y -= dy * 5;

        hunter2X += dx * 5;

        hunter2Y += dy * 5;

    }

    private void setHunterDashDirection(int hunter, double dx, double dy) {

        double len = Math.sqrt(dx * dx + dy * dy);

        if (len == 0) return;

        if (hunter == 1) {

            hunter1DashDirX = dx / len;

            hunter1DashDirY = dy / len;

        } else {

            hunter2DashDirX = dx / len;

            hunter2DashDirY = dy / len;

        }

    }

    private void launchHunterAway(

        int hunter, double fromX, double fromY, double strength

    ) {

        double hx;

        double hy;

        if (hunter == 1) {

            hx = hunter1X + HUNTER_SIZE / 2.0;

            hy = hunter1Y + HUNTER_SIZE / 2.0;

        } else {

            hx = hunter2X + HUNTER_SIZE / 2.0;

            hy = hunter2Y + HUNTER_SIZE / 2.0;

        }

        double dx = hx - fromX;

        double dy = hy - fromY;

        double len = Math.sqrt(dx * dx + dy * dy);

        if (len == 0) {

            dx = 1;

            dy = 0;

            len = 1;

        }

        dx /= len;

        dy /= len;

        double vx = dx * HUNTER_LAUNCH_SPEED * strength;

        double vy = dy * HUNTER_LAUNCH_SPEED * strength;

        if (hunter == 1) {

            hunter1VX = vx;

            hunter1VY = vy;

            hunter1DashDirX = dx;

            hunter1DashDirY = dy;

            hunter1DashTime = 0.22;

            hunter1DashCooldown = HUNTER_DASH_COOLDOWN;

        } else {

            hunter2VX = vx;

            hunter2VY = vy;

            hunter2DashDirX = dx;

            hunter2DashDirY = dy;

            hunter2DashTime = 0.22;

            hunter2DashCooldown = HUNTER_DASH_COOLDOWN;

        }

    }

    // ---------------- ELIMINATION AND RESPAWNING ----------------

    private void eliminateHunter(int hunter) {

        if (hunter == 1 && hunter1Alive) {

            hunter1Alive = false;

            hunter1RespawnTimer = HUNTER_RESPAWN_DELAY;

            hunter1DashTime = 0;

            hunter1VX = 0;

            hunter1VY = 0;

            showMessage("Hunter 1 eliminated! Respawning in 15 seconds.");

        } else if (hunter == 2 && hunter2Alive) {

            hunter2Alive = false;

            hunter2RespawnTimer = HUNTER_RESPAWN_DELAY;

            hunter2DashTime = 0;

            hunter2VX = 0;

            hunter2VY = 0;

            showMessage("Hunter 2 eliminated! Respawning in 15 seconds.");

        }

    }

    private void updateRespawnTimers(double dt) {

        if (!hunter1Alive) {

            hunter1RespawnTimer -= dt;

            if (hunter1RespawnTimer <= 0) {

                respawnHunter(1);

            }

        }

        if (!hunter2Alive) {

            hunter2RespawnTimer -= dt;

            if (hunter2RespawnTimer <= 0) {

                respawnHunter(2);

            }

        }

    }

    private void respawnHunter(int hunter) {

        double[] pos = findSafeSpawn(HUNTER_SIZE);

        if (hunter == 1) {

            hunter1X = pos[0];

            hunter1Y = pos[1];

            hunter1VX = 0;

            hunter1VY = 0;

            hunter1Speed = HUNTER_START_SPEED;

            hunter1DashTime = 0;

            hunter1DashCooldown = 1.0;

            hunter1StunTime = 0;
            hunter1WallJumpTime = 0;

            hunter1Alive = true;

            showMessage("Hunter 1 has respawned!");

        } else {

            hunter2X = pos[0];

            hunter2Y = pos[1];

            hunter2VX = 0;

            hunter2VY = 0;

            hunter2Speed = HUNTER_START_SPEED;

            hunter2DashTime = 0;

            hunter2DashCooldown = 1.0;

            hunter2StunTime = 0;
            hunter2WallJumpTime = 0;

            hunter2Alive = true;

            showMessage("Hunter 2 has respawned!");

        }

    }

    private double[] findSafeSpawn(int size) {

        for (int attempt = 0; attempt < 200; attempt++) {

            double x = BORDER + 10

                + random.nextInt(WIDTH - 2 * BORDER - size - 20);

            double y = BORDER + 10

                + random.nextInt(HEIGHT - 2 * BORDER - size - 20);

            if (hitsWall(x, y, size)) continue;

            if (distance(x, y, playerX, playerY) < 180) continue;

            if (hunter1Alive &&

                distance(x, y, hunter1X, hunter1Y) < 70) continue;

            if (hunter2Alive &&

                distance(x, y, hunter2X, hunter2Y) < 70) continue;

            return new double[] {x, y};

        }

        // Fallback spawn positions are in open parts of the arena.

        return new double[] {WIDTH - 100, HEIGHT - 100};

    }

    // ---------------- PATHFINDING AND COLLISION ----------------

    private boolean hasLineOfSight(

        double x1, double y1, double x2, double y2

    ) {

        double dx = x2 - x1;

        double dy = y2 - y1;

        double len = Math.sqrt(dx * dx + dy * dy);

        if (len == 0) return true;

        int steps = Math.max(1, (int) (len / 5));

        for (int i = 1; i < steps; i++) {

            double t = (double) i / steps;

            if (pointInsideWall(x1 + dx * t, y1 + dy * t)) {

                return false;

            }

        }

        return true;

    }

    private boolean pointInsideWall(double x, double y) {

        if (x < BORDER || y < BORDER

                || x > WIDTH - BORDER || y > HEIGHT - BORDER) {

            return true;

        }

        for (Rectangle wall : walls) {

            if (wall.contains(x, y)) return true;

        }

        return false;

    }

    private boolean isDashPathClear(

        double x, double y,

        double dx, double dy,

        int size, double dashDistance

    ) {

        int steps = Math.max(1, (int) (dashDistance / 4));

        for (int i = 1; i <= steps; i++) {

            double d = dashDistance * i / steps;

            if (hitsWall(x + dx * d, y + dy * d, size)) {

                return false;

            }

        }

        return true;

    }

    private double[] findPath(

        double x, double y,

        double targetX, double targetY,

        int size

    ) {

        double bestX = 0;

        double bestY = 0;

        double bestScore = Double.MAX_VALUE;

        double[] directions = {-1, -0.5, 0, 0.5, 1};

        for (double dx : directions) {

            for (double dy : directions) {

                if (dx == 0 && dy == 0) continue;

                double len = Math.sqrt(dx * dx + dy * dy);

                double ndx = dx / len;

                double ndy = dy / len;

                double testX = x + ndx * 35 - size / 2.0;

                double testY = y + ndy * 35 - size / 2.0;

                if (hitsWall(testX, testY, size)) continue;

                double futureX = x + ndx * 110;

                double futureY = y + ndy * 110;

                double score = distance(

                    futureX, futureY, targetX, targetY

                );

                if (!isDashPathClear(

                    x - size / 2.0, y - size / 2.0,

                    ndx, ndy, size, 65)) {

                    score += 100;

                }

                if (score < bestScore) {

                    bestScore = score;

                    bestX = ndx;

                    bestY = ndy;

                }

            }

        }

        return new double[] {bestX, bestY};

    }

    // Arena boundaries are not jumpable; internal walls are.
    private boolean hitsArenaBoundary(double x, double y, int size) {
        return x < BORDER || y < BORDER
            || x + size > WIDTH - BORDER
            || y + size > HEIGHT - BORDER;
    }

    private boolean hitsInternalWall(double x, double y, int size) {
        Rectangle object = new Rectangle((int) x, (int) y, size, size);
        for (Rectangle wall : walls) {
            if (object.intersects(wall)) return true;
        }
        return false;
    }

    // Move through the internal wall in the dash direction, then briefly phase.
    private double[] wallJumpDestination(double x, double y, int size,
            double dirX, double dirY) {
        double len = Math.sqrt(dirX * dirX + dirY * dirY);
        if (len == 0) return null;
        dirX /= len;
        dirY /= len;
        boolean enteredWall = false;
        for (int distance = 4; distance <= 220; distance += 4) {
            double nx = x + dirX * distance;
            double ny = y + dirY * distance;
            if (hitsArenaBoundary(nx, ny, size)) return null;
            if (hitsInternalWall(nx, ny, size)) {
                enteredWall = true;
            } else if (enteredWall) {
                // Only land after we've crossed through the internal wall.
                return new double[] {nx, ny};
            }
        }
        return null;
    }

    private void updateWallJumpAnimations(double dt) {
        final double duration = 0.48;
        if (playerWallJumpTime > 0) {
            playerWallJumpTime = Math.max(0, playerWallJumpTime - dt);
            double t = 1.0 - playerWallJumpTime / duration;
            // Smoothly slide along the dash direction, rather than teleporting.
            double eased = t * t * (3 - 2 * t);
            playerX = playerWallJumpStartX + (playerWallJumpTargetX - playerWallJumpStartX) * eased;
            playerY = playerWallJumpStartY + (playerWallJumpTargetY - playerWallJumpStartY) * eased;
            if (playerWallJumpTime == 0) { playerX = playerWallJumpTargetX; playerY = playerWallJumpTargetY; }
        }
        if (hunter1WallJumpTime > 0) {
            hunter1WallJumpTime = Math.max(0, hunter1WallJumpTime - dt);
            double t = 1.0 - hunter1WallJumpTime / duration;
            double eased = t * t * (3 - 2 * t);
            hunter1X = hunter1WallJumpStartX + (hunter1WallJumpTargetX - hunter1WallJumpStartX) * eased;
            hunter1Y = hunter1WallJumpStartY + (hunter1WallJumpTargetY - hunter1WallJumpStartY) * eased;
            if (hunter1WallJumpTime == 0) { hunter1X = hunter1WallJumpTargetX; hunter1Y = hunter1WallJumpTargetY; }
        }
        if (hunter2WallJumpTime > 0) {
            hunter2WallJumpTime = Math.max(0, hunter2WallJumpTime - dt);
            double t = 1.0 - hunter2WallJumpTime / duration;
            double eased = t * t * (3 - 2 * t);
            hunter2X = hunter2WallJumpStartX + (hunter2WallJumpTargetX - hunter2WallJumpStartX) * eased;
            hunter2Y = hunter2WallJumpStartY + (hunter2WallJumpTargetY - hunter2WallJumpStartY) * eased;
            if (hunter2WallJumpTime == 0) { hunter2X = hunter2WallJumpTargetX; hunter2Y = hunter2WallJumpTargetY; }
        }
    }

    private boolean tryPlayerWallJump() {
        double[] destination = wallJumpDestination(playerX, playerY, PLAYER_SIZE,
            playerDashDirX, playerDashDirY);
        if (destination == null) return false;
        playerWallJumpStartX = playerX;
        playerWallJumpStartY = playerY;
        playerWallJumpTargetX = destination[0];
        playerWallJumpTargetY = destination[1];
        playerDashTime = 0;
        playerWallJumpTime = 0.48;
        playerVX = 0;
        playerVY = 0;
        showMessage("Wall jump!");
        return true;
    }

    private boolean tryHunterWallJump(int hunter) {
        double x = hunter == 1 ? hunter1X : hunter2X;
        double y = hunter == 1 ? hunter1Y : hunter2Y;
        double dirX = hunter == 1 ? hunter1DashDirX : hunter2DashDirX;
        double dirY = hunter == 1 ? hunter1DashDirY : hunter2DashDirY;
        double[] destination = wallJumpDestination(x, y, HUNTER_SIZE, dirX, dirY);
        if (destination == null) return false;
        if (hunter == 1) {
            hunter1WallJumpStartX = hunter1X; hunter1WallJumpStartY = hunter1Y;
            hunter1WallJumpTargetX = destination[0]; hunter1WallJumpTargetY = destination[1];
            hunter1DashTime = 0; hunter1WallJumpTime = 0.48;
            hunter1VX = 0; hunter1VY = 0;
        } else {
            hunter2WallJumpStartX = hunter2X; hunter2WallJumpStartY = hunter2Y;
            hunter2WallJumpTargetX = destination[0]; hunter2WallJumpTargetY = destination[1];
            hunter2DashTime = 0; hunter2WallJumpTime = 0.48;
            hunter2VX = 0; hunter2VY = 0;
        }
        return true;
    }

    private boolean hitsWall(double x, double y, int size) {

        if (x < BORDER || y < BORDER

                || x + size > WIDTH - BORDER

                || y + size > HEIGHT - BORDER) {

            return true;

        }

        Rectangle object = new Rectangle(

            (int) x, (int) y, size, size

        );

        for (Rectangle wall : walls) {

            if (object.intersects(wall)) return true;

        }

        return false;

    }

    private void updateNearbyCash(double dt) {
        double px = playerX + PLAYER_SIZE / 2.0;
        double py = playerY + PLAYER_SIZE / 2.0;
        boolean near = (hunter1Alive && distance(px, py, hunter1X + HUNTER_SIZE / 2.0, hunter1Y + HUNTER_SIZE / 2.0) <= HUNTER_NEARBY_RADIUS)
            || (hunter2Alive && distance(px, py, hunter2X + HUNTER_SIZE / 2.0, hunter2Y + HUNTER_SIZE / 2.0) <= HUNTER_NEARBY_RADIUS);
        if (near) {
            nearbyCashAccumulator += dt;
            while (nearbyCashAccumulator >= 1.0) {
                cash += 5;
                nearbyCashAccumulator -= 1.0;
                showMessage("+$5 for staying near a hunter!");
            }
        } else {
            nearbyCashAccumulator = 0;
        }
    }

    private void endRound() {
        roundsCompleted++;
        prepareUpgradeChoices();
        cash += 50;
        phase = cash >= ITEM_PRICE && heldItem == null ? GamePhase.SHOP : GamePhase.UPGRADE;
        roundTimer = ROUND_LENGTH;
        extraChanceAvailable = extraChanceUpgrade;
        extraChanceUsed = false;
        showMessage("Round complete! +$50");
    }

    private void handlePlayerCaught() {
        if (extraChanceAvailable && !extraChanceUsed) {
            extraChanceUsed = true;
            extraChanceAvailable = false;
            playerX = 80;
            playerY = 80;
            playerVX = 0;
            playerVY = 0;
            playerDashTime = 0;
            playerStunTime = 0;
            playerInvulnerable = true;
            invulnerabilityTime = 2.0;
            showMessage("Extra Chance used! You have returned to the arena.");
        } else {
            gameOver = true;
            bestTime = Math.max(bestTime, survivalTime);
        }
    }

    private void chooseShopItem(int choice) {
        if (phase != GamePhase.SHOP) return;
        if (heldItem != null) {
            showMessage("Use your current item before buying another!");
            return;
        }
        if (cash < ITEM_PRICE) {
            showMessage("You need $100 to buy an item.");
            return;
        }
        ItemType[] types = ItemType.values();
        if (choice < 1 || choice > types.length) return;
        heldItem = types[choice - 1];
        cash -= ITEM_PRICE;
        phase = GamePhase.UPGRADE;
        showMessage("Bought " + itemName(heldItem) + " for $100!");
    }

    private void prepareUpgradeChoices() {
        List<Integer> choices = new ArrayList<>();
        for (int i = 1; i <= 5; i++) choices.add(i);
        for (int i = choices.size() - 1; i > 0; i--) {
            int j = random.nextInt(i + 1);
            int temp = choices.get(i); choices.set(i, choices.get(j)); choices.set(j, temp);
        }
        currentUpgradeChoices = new int[] {choices.get(0), choices.get(1), choices.get(2)};
    }

    private void chooseUpgrade(int choice) {
        if (phase != GamePhase.UPGRADE || choice < 1 || choice > 3) return;
        int selected = currentUpgradeChoices[choice - 1];
        if (selected == 1) {
            extraChanceUpgrade = true;
            extraChanceAvailable = true;
            extraChanceUsed = false;
            showMessage("Extra Chance selected!");
        } else if (selected == 2) {
            gluedShoes = true;
            showMessage("Glued Shoes selected! Hunters accelerate more slowly.");
        } else if (selected == 3) {
            dashOnDash = true;
            showMessage("Dashs on Dashs selected! Dash refresh has a 2-second cooldown.");
        } else if (selected == 4) {
            marioJump = true;
            showMessage("Mario Jump selected! Dash over a hunter to stun them.");
        } else if (selected == 5) {
            roomOfMirrors = true;
            showMessage("Room of Mirrors selected! Dash through a mirror to teleport.");
        } else {
            return;
        }
        phase = GamePhase.PLAYING;
        hunter1Speed = HUNTER_START_SPEED;
        hunter2Speed = HUNTER_START_SPEED;
        hunter1VX = hunter1VY = hunter2VX = hunter2VY = 0;
        roundTimer = ROUND_LENGTH;
        extraChanceAvailable = extraChanceUpgrade;
        extraChanceUsed = false;
        showMessage("Round " + (roundsCompleted + 1) + " begins!");
    }

    private void checkPlayerCollision() {
        if (playerDashTime > 0 && dashOnDash && dashRefreshTimer <= 0) {
            Rectangle dashingPlayer = new Rectangle((int) playerX, (int) playerY, PLAYER_SIZE, PLAYER_SIZE);
            if ((hunter1Alive && dashingPlayer.intersects(new Rectangle((int) hunter1X, (int) hunter1Y, HUNTER_SIZE, HUNTER_SIZE))) ||
                (hunter2Alive && dashingPlayer.intersects(new Rectangle((int) hunter2X, (int) hunter2Y, HUNTER_SIZE, HUNTER_SIZE)))) {
                playerDashCooldown = 0;
                dashRefreshTimer = DASH_REFRESH_COOLDOWN;
                showMessage("Dash refreshed!");
            }
        }
        if (playerDashTime > 0 && marioJump) {
            Rectangle jumpingPlayer = new Rectangle((int) playerX, (int) playerY, PLAYER_SIZE, PLAYER_SIZE);
            if (hunter1Alive && jumpingPlayer.intersects(new Rectangle((int) hunter1X, (int) hunter1Y, HUNTER_SIZE, HUNTER_SIZE))
                    && playerY + PLAYER_SIZE / 2.0 < hunter1Y + HUNTER_SIZE / 2.0) {
                hunter1StunTime = Math.max(hunter1StunTime, 1.5); hunter1DashTime = 0;
                playerDashTime = 0; showMessage("Mario Jump! Hunter stunned!");
            } else if (hunter2Alive && jumpingPlayer.intersects(new Rectangle((int) hunter2X, (int) hunter2Y, HUNTER_SIZE, HUNTER_SIZE))
                    && playerY + PLAYER_SIZE / 2.0 < hunter2Y + HUNTER_SIZE / 2.0) {
                hunter2StunTime = Math.max(hunter2StunTime, 1.5); hunter2DashTime = 0;
                playerDashTime = 0; showMessage("Mario Jump! Hunter stunned!");
            }
        }
        if (playerDashTime > 0 || playerInvulnerable) return;

        Rectangle player = new Rectangle(

            (int) playerX, (int) playerY,

            PLAYER_SIZE, PLAYER_SIZE

        );

        if (hunter1Alive && hunter1StunTime <= 0 && player.intersects(new Rectangle(

                (int) hunter1X, (int) hunter1Y,

                HUNTER_SIZE, HUNTER_SIZE))) {

            if (shieldActive && hunter1DashTime > 0) {

                shieldActive = false;

                launchHunterAway(

                    1,

                    playerX + PLAYER_SIZE / 2.0,

                    playerY + PLAYER_SIZE / 2.0,

                    1.0

                );

                showMessage("Shield blocked Hunter 1's dash!");

            } else {

                handlePlayerCaught();

            }

        }

        if (hunter2Alive && hunter2StunTime <= 0 && player.intersects(new Rectangle(

                (int) hunter2X, (int) hunter2Y,

                HUNTER_SIZE, HUNTER_SIZE))) {

            if (shieldActive && hunter2DashTime > 0) {

                shieldActive = false;

                launchHunterAway(

                    2,

                    playerX + PLAYER_SIZE / 2.0,

                    playerY + PLAYER_SIZE / 2.0,

                    1.0

                );

                showMessage("Shield blocked Hunter 2's dash!");

            } else {

                handlePlayerCaught();

            }

        }

    }

    private void moveHunterOne(double dx, double dy) {
        if (roomOfMirrors && hunter1Alive && hunter1DashTime > 0) {
            Rectangle hunterRect = new Rectangle((int) hunter1X, (int) hunter1Y, HUNTER_SIZE, HUNTER_SIZE);
            for (Rectangle mirror : mirrors) {
                if (hunterRect.intersects(mirror)) {
                    hunter1DashTime = 0;
                    hunter1StunTime = Math.max(hunter1StunTime, 0.75);
                    showMessage("Hunter stunned by a mirror!");
                    break;
                }
            }
        }
        if (!hunter1Alive || hunter1WallJumpTime > 0) return;
        boolean dashing = hunter1DashTime > 0;
        double nx = hunter1X + dx;
        if (hitsArenaBoundary(nx, hunter1Y, HUNTER_SIZE)) {
            hunter1VX = 0;
            if (dashing) { hunter1DashTime = 0; hunter1StunTime = 0.35; }
        } else if (hitsInternalWall(nx, hunter1Y, HUNTER_SIZE)) {
            if (dashing && tryHunterWallJump(1)) return;
            hunter1VX = 0;
            if (dashing) { hunter1DashTime = 0; hunter1StunTime = 0.35; }
        } else hunter1X = nx;

        double ny = hunter1Y + dy;
        if (hitsArenaBoundary(hunter1X, ny, HUNTER_SIZE)) {
            hunter1VY = 0;
            if (dashing) { hunter1DashTime = 0; hunter1StunTime = 0.35; }
        } else if (hitsInternalWall(hunter1X, ny, HUNTER_SIZE)) {
            if (dashing && tryHunterWallJump(1)) return;
            hunter1VY = 0;
            if (dashing) { hunter1DashTime = 0; hunter1StunTime = 0.35; }
        } else hunter1Y = ny;
    }

    private void moveHunterTwo(double dx, double dy) {
        if (roomOfMirrors && hunter2Alive && hunter2DashTime > 0) {
            Rectangle hunterRect = new Rectangle((int) hunter2X, (int) hunter2Y, HUNTER_SIZE, HUNTER_SIZE);
            for (Rectangle mirror : mirrors) {
                if (hunterRect.intersects(mirror)) {
                    hunter2DashTime = 0;
                    hunter2StunTime = Math.max(hunter2StunTime, 0.75);
                    showMessage("Hunter stunned by a mirror!");
                    break;
                }
            }
        }
        if (!hunter2Alive || hunter2WallJumpTime > 0) return;
        boolean dashing = hunter2DashTime > 0;
        double nx = hunter2X + dx;
        if (hitsArenaBoundary(nx, hunter2Y, HUNTER_SIZE)) {
            hunter2VX = 0;
            if (dashing) { hunter2DashTime = 0; hunter2StunTime = 0.35; }
        } else if (hitsInternalWall(nx, hunter2Y, HUNTER_SIZE)) {
            if (dashing && tryHunterWallJump(2)) return;
            hunter2VX = 0;
            if (dashing) { hunter2DashTime = 0; hunter2StunTime = 0.35; }
        } else hunter2X = nx;

        double ny = hunter2Y + dy;
        if (hitsArenaBoundary(hunter2X, ny, HUNTER_SIZE)) {
            hunter2VY = 0;
            if (dashing) { hunter2DashTime = 0; hunter2StunTime = 0.35; }
        } else if (hitsInternalWall(hunter2X, ny, HUNTER_SIZE)) {
            if (dashing && tryHunterWallJump(2)) return;
            hunter2VY = 0;
            if (dashing) { hunter2DashTime = 0; hunter2StunTime = 0.35; }
        } else hunter2Y = ny;
    }

    private double distance(

        double x1, double y1, double x2, double y2

    ) {

        double dx = x2 - x1;

        double dy = y2 - y1;

        return Math.sqrt(dx * dx + dy * dy);

    }

    private String itemName(ItemType type) {

        switch (type) {

            case SHIELD: return "Impact Shield";

            case SHOCKWAVE: return "Shockwave";

            case SNARE_MINE: return "Snare Mine";

            case OVERDRIVE: return "Overdrive";

            case PHASE_SHIFT: return "Phase Shift";

            default: return "Unknown";

        }

    }

    private Color itemColor(ItemType type) {

        switch (type) {

            case SHIELD: return Color.CYAN;

            case SHOCKWAVE: return new Color(180, 60, 255);

            case SNARE_MINE: return Color.ORANGE;

            case OVERDRIVE: return Color.GREEN;

            case PHASE_SHIFT: return new Color(70, 160, 255);

            default: return Color.WHITE;

        }

    }

    private void showMessage(String text) {

        message = text;

        messageTimer = 2.5;

    }

    // ---------------- RESTART ----------------

    private void restart() {

        playerX = 80;

        playerY = 80;

        playerVX = 0;

        playerVY = 0;

        playerDashTime = 0;

        playerDashCooldown = 0;

        playerStunTime = 0;
        playerWallJumpTime = 0;

        playerOverdriveTime = 0;

        shieldActive = false;

        playerInvulnerable = false;

        invulnerabilityTime = 0;

        heldItem = null;

        hunter1X = 950;

        hunter1Y = 100;

        hunter1VX = 0;

        hunter1VY = 0;

        hunter1Speed = HUNTER_START_SPEED;

        hunter1DashTime = 0;

        hunter1DashCooldown = 0;
        hunter1TimeSinceDash = 0;

        hunter1StunTime = 0;

        hunter1RespawnTimer = 0;

        hunter1Alive = true;

        hunter2X = 950;

        hunter2Y = 600;

        hunter2VX = 0;

        hunter2VY = 0;

        hunter2Speed = HUNTER_START_SPEED;

        hunter2DashTime = 0;

        hunter2DashCooldown = 0;
        hunter2TimeSinceDash = 0;

        hunter2StunTime = 0;

        hunter2RespawnTimer = 0;

        hunter2Alive = true;

        snares.clear();

        roundTimer = ROUND_LENGTH;
        cash = 0;
        nearbyCashAccumulator = 0;
        dashRefreshTimer = 0;
        roundsCompleted = 0;
        phase = GamePhase.PLAYING;
        extraChanceUpgrade = false;
        extraChanceAvailable = false;
        extraChanceUsed = false;
        gluedShoes = false;
        dashOnDash = false;
        dashHitHunterThisDash = false;
        marioJump = false;
        roomOfMirrors = false;
        prepareUpgradeChoices();

        survivalTime = 0;

        gameOver = false;

        dashPressed = false;

        useItemPressed = false;

        requestFocusInWindow();

    }

    // ---------------- DRAWING ----------------

    @Override

    protected void paintComponent(Graphics g) {

        super.paintComponent(g);

        Graphics2D g2 = (Graphics2D) g;

        g2.setRenderingHint(

            RenderingHints.KEY_ANTIALIASING,

            RenderingHints.VALUE_ANTIALIAS_ON

        );

        g2.setColor(Color.RED);

        g2.setStroke(new BasicStroke(BORDER));

        g2.drawRect(

            BORDER / 2, BORDER / 2,

            WIDTH - BORDER, HEIGHT - BORDER

        );

        g2.setColor(new Color(90, 90, 105));

        for (Rectangle wall : walls) {

            g2.fill(wall);

        }

        if (roomOfMirrors) {
            for (Rectangle mirror : mirrors) {
                g2.setColor(new Color(100, 220, 255));
                g2.fillRoundRect(mirror.x, mirror.y, mirror.width, mirror.height, 10, 10);
                g2.setColor(Color.WHITE);
                g2.drawRoundRect(mirror.x, mirror.y, mirror.width, mirror.height, 10, 10);
            }
        }

        // Draw snare mines.

        for (Snare snare : snares) {

            g2.setColor(Color.ORANGE);

            g2.fillOval(

                (int) snare.x - 12,

                (int) snare.y - 12, 24, 24

            );

            g2.setColor(Color.WHITE);

            g2.drawOval(

                (int) snare.x - 12,

                (int) snare.y - 12, 24, 24

            );

        }

        // Draw player; fade during the wall-jump phase animation.
        if (playerWallJumpTime > 0) {
            float alpha = (float) (0.20 + 0.65 * Math.abs(Math.sin(playerWallJumpTime * 18)));
            g2.setComposite(AlphaComposite.getInstance(AlphaComposite.SRC_OVER, alpha));
        }
        g2.setColor(playerStunTime > 0 ? Color.YELLOW : Color.CYAN);

        g2.fillOval(

            (int) playerX, (int) playerY,

            PLAYER_SIZE, PLAYER_SIZE

        );

        g2.setComposite(AlphaComposite.SrcOver);

        if (shieldActive) {

            g2.setColor(Color.CYAN);

            g2.setStroke(new BasicStroke(3));

            g2.drawOval(

                (int) playerX - 5, (int) playerY - 5,

                PLAYER_SIZE + 10, PLAYER_SIZE + 10

            );

        }

        if (playerInvulnerable) {

            g2.setColor(Color.WHITE);

            g2.drawOval(

                (int) playerX - 8, (int) playerY - 8,

                PLAYER_SIZE + 16, PLAYER_SIZE + 16

            );

        }

        // Draw hunters, including respawn countdowns.

        if (hunter1Alive) {

            if (hunter1WallJumpTime > 0) {
                float alpha = (float) (0.20 + 0.65 * Math.abs(Math.sin(hunter1WallJumpTime * 18)));
                g2.setComposite(AlphaComposite.getInstance(AlphaComposite.SRC_OVER, alpha));
            }
            g2.setColor(hunter1StunTime > 0

                ? Color.ORANGE : Color.RED);

            g2.fillRoundRect(

                (int) hunter1X, (int) hunter1Y,

                HUNTER_SIZE, HUNTER_SIZE, 8, 8

            );
            g2.setComposite(AlphaComposite.SrcOver);

        } else {

            g2.setColor(Color.LIGHT_GRAY);

            g2.drawString(

                String.format("Hunter 1: %.1fs", hunter1RespawnTimer),

                35, 100

            );

        }

        if (hunter2Alive) {

            if (hunter2WallJumpTime > 0) {
                float alpha = (float) (0.20 + 0.65 * Math.abs(Math.sin(hunter2WallJumpTime * 18)));
                g2.setComposite(AlphaComposite.getInstance(AlphaComposite.SRC_OVER, alpha));
            }
            g2.setColor(hunter2StunTime > 0

                ? Color.ORANGE : new Color(180, 60, 255));

            g2.fillRoundRect(

                (int) hunter2X, (int) hunter2Y,

                HUNTER_SIZE, HUNTER_SIZE, 8, 8

            );
            g2.setComposite(AlphaComposite.SrcOver);

        } else {

            g2.setColor(Color.LIGHT_GRAY);

            g2.drawString(

                String.format("Hunter 2: %.1fs", hunter2RespawnTimer),

                35, 120

            );

        }

        // HUD.

        g2.setColor(Color.WHITE);

        g2.setFont(new Font("Arial", Font.BOLD, 20));

        g2.drawString(

            String.format("Survival: %.1f seconds", survivalTime),

            35, 45

        );

        g2.setFont(new Font("Arial", Font.PLAIN, 14));

        g2.drawString(

            String.format("Best: %.1f seconds", bestTime),

            35, 68

        );

        g2.drawString(

            "Move: WASD / Arrows    Dash: Q    Use item: E",

            35, HEIGHT - 45

        );

        g2.drawString(String.format("Cash: $%d", cash), WIDTH - 220, 45);
        g2.drawString(String.format("Round ends in: %.1f", roundTimer), WIDTH - 220, 92);

        g2.drawString(

            String.format("Hunter speed: %.0f / %.0f",

                Math.max(hunter1Speed, hunter2Speed),

                HUNTER_MAX_SPEED),

            WIDTH - 220, 68

        );

        g2.setFont(new Font("Arial", Font.BOLD, 16));

        if (heldItem == null) {

            g2.setColor(Color.LIGHT_GRAY);

            g2.drawString("Held item: None", WIDTH - 220, 120);

        } else {

            g2.setColor(itemColor(heldItem));

            g2.drawString(

                "Held item: " + itemName(heldItem),

                WIDTH - 250, 120

            );

        }

        if (shieldActive) {

            g2.setColor(Color.CYAN);

            g2.drawString("Shield ready!", WIDTH - 220, 145);

        }

        if (playerOverdriveTime > 0) {

            g2.setColor(Color.GREEN);

            g2.drawString(

                String.format("Overdrive: %.1fs", playerOverdriveTime),

                WIDTH - 220, 150

            );

        }

        if (messageTimer > 0) {

            g2.setColor(Color.WHITE);

            g2.setFont(new Font("Arial", Font.BOLD, 18));

            drawCentered(g2, message, HEIGHT - 75);

        }

        if (phase == GamePhase.SHOP || phase == GamePhase.UPGRADE) {
            g2.setColor(new Color(0, 0, 0, 220));
            g2.fillRect(0, 0, WIDTH, HEIGHT);
            g2.setColor(Color.WHITE);
            g2.setFont(new Font("Arial", Font.BOLD, 42));
            drawCentered(g2, phase == GamePhase.SHOP ? "SHOP INTERMISSION" : "CHOOSE AN UPGRADE", HEIGHT / 2 - 170);
            g2.setFont(new Font("Arial", Font.BOLD, 23));
            drawCentered(g2, "Cash: $" + cash, HEIGHT / 2 - 125);
            g2.setFont(new Font("Arial", Font.PLAIN, 19));
            if (phase == GamePhase.SHOP) {
                drawCentered(g2, "Choose ONE item for $100 (press 1-5):", HEIGHT / 2 - 75);
                drawCentered(g2, "1. Impact Shield    2. Shockwave    3. Snare Mine", HEIGHT / 2 - 35);
                drawCentered(g2, "4. Overdrive    5. Phase Shift", HEIGHT / 2 + 5);
                drawCentered(g2, "Press SPACE to skip shopping", HEIGHT / 2 + 65);
            } else {
                for (int i = 0; i < 3; i++) {
                    String description;
                    switch (currentUpgradeChoices[i]) {
                        case 1: description = "Extra Chance - one extra life each round"; break;
                        case 2: description = "Glued Shoes - hunters accelerate 65% slower"; break;
                        case 3: description = "Dashs on Dashs - dash hit refresh (2s cooldown)"; break;
                        case 4: description = "Mario Jump - dash over a hunter to stun them 1.5s"; break;
                        default: description = "Room of Mirrors - dash through mirrors to teleport"; break;
                    }
                    drawCentered(g2, (i + 1) + ". " + description, HEIGHT / 2 - 65 + i * 45);
                }
            }
        }

        if (gameOver) {

            g2.setColor(new Color(0, 0, 0, 190));

            g2.fillRect(0, 0, WIDTH, HEIGHT);

            g2.setColor(Color.WHITE);

            g2.setFont(new Font("Arial", Font.BOLD, 52));

            drawCentered(g2, "CAUGHT!", HEIGHT / 2 - 35);

            g2.setFont(new Font("Arial", Font.PLAIN, 25));

            drawCentered(

                g2,

                String.format("You survived %.1f seconds", survivalTime),

                HEIGHT / 2 + 10

            );

            g2.setFont(new Font("Arial", Font.PLAIN, 20));

            drawCentered(g2, "Press R to try again", HEIGHT / 2 + 55);

        }

    }

    private String itemLetter(ItemType type) {

        switch (type) {

            case SHIELD: return "S";

            case SHOCKWAVE: return "W";

            case SNARE_MINE: return "M";

            case OVERDRIVE: return "O";

            case PHASE_SHIFT: return "P";

            default: return "?";

        }

    }

    private void drawCentered(Graphics2D g2, String text, int y) {

        FontMetrics metrics = g2.getFontMetrics();

        g2.drawString(

            text,

            (WIDTH - metrics.stringWidth(text)) / 2,

            y

        );

    }

    // ---------------- KEYBOARD ----------------

    @Override

    public void keyPressed(KeyEvent e) {

        int key = e.getKeyCode();

        if (key >= 0 && key < keys.length) {

            keys[key] = true;

        }

        if (key == KeyEvent.VK_Q) {

            dashPressed = true;

        }

        if (key == KeyEvent.VK_E) {

            useItemPressed = true;

        }

        if (key == KeyEvent.VK_R && gameOver) {
            restart();
        }
        if (key == KeyEvent.VK_T && phase == GamePhase.PLAYING && !gameOver) {
            endRound();
        }
        if (phase == GamePhase.SHOP) {
            if (key >= KeyEvent.VK_1 && key <= KeyEvent.VK_5) chooseShopItem(key - KeyEvent.VK_0);
            if (key == KeyEvent.VK_SPACE) phase = GamePhase.UPGRADE;
        } else if (phase == GamePhase.UPGRADE) {
            if (key >= KeyEvent.VK_1 && key <= KeyEvent.VK_3) chooseUpgrade(key - KeyEvent.VK_0);
        }

    }

    @Override

    public void keyReleased(KeyEvent e) {

        int key = e.getKeyCode();

        if (key >= 0 && key < keys.length) {

            keys[key] = false;

        }

    }

    @Override

    public void keyTyped(KeyEvent e) {

        // Not needed.

    }

    public static void main(String[] args) {

        SwingUtilities.invokeLater(() -> {

            JFrame frame = new JFrame("Learning Hunter");

            LearningHunter game = new LearningHunter();

            frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);

            frame.setResizable(false);

            frame.add(game);

            frame.pack();

            frame.setLocationRelativeTo(null);

            frame.setVisible(true);

            game.requestFocusInWindow();

        });

    }

}
}
3.
public class FirstArray extends ConsoleProgram
{
    public void run()
    {
        int[] firstArray = {2,4,6,8,10};
        System.out.println(firstArray[1]);
        System.out.println(firstArray[3]);
    }
}



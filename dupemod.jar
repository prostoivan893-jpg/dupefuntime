package com.example.dupe;

import net.fabricmc.api.ModInitializer;
import net.fabricmc.fabric.api.command.v2.CommandRegistrationCallback;
import net.minecraft.server.command.CommandManager;
import net.minecraft.server.network.ServerPlayerEntity;
import net.minecraft.item.ItemStack;
import net.minecraft.text.Text;
import net.minecraft.util.Formatting;

public class DupeMod implements ModInitializer {

    @Override
    public void onInitialize() {
        // Регистрация команды /dupe
        CommandRegistrationCallback.EVENT.register((dispatcher, registryAccess, environment) -> {
            dispatcher.register(CommandManager.literal("dupe")
                .executes(context -> {
                    ServerPlayerEntity player = context.getSource().getPlayer();

                    if (player == null) return 0;

                    // Берем предмет из левой руки
                    ItemStack offhandStack = player.getOffHandStack();

                    if (offhandStack.isEmpty()) {
                        player.sendMessage(Text.literal("Левая рука пуста!")
                            .formatted(Formatting.RED), false);
                        return 0;
                    }

                    // Создаем копию
                    ItemStack dupeStack = offhandStack.copy();
                    
                    // Выдаем игроку
                    if (!player.getInventory().insertStack(dupeStack)) {
                        // Если инвентарь полон — выкидываем рядом
                        player.dropItem(dupeStack, false);
                    }

                    player.sendMessage(Text.literal("Предмет размножен!")
                        .formatted(Formatting.GREEN), false);
                    
                    return 1;
                })
            );
        });
    }
}


import React, { useState } from "react";
import {
  SafeAreaView,
  View,
  Text,
  TextInput,
  TouchableOpacity,
  ScrollView,
  StyleSheet,
} from "react-native";

export default function App() {
  const [message, setMessage] = useState("");
  const [messages, setMessages] = useState([
    {
      role: "sidekick",
      text: "I'm here. We can talk, think, plan, or figure something out together. What’s on your mind?",
    },
  ]);
  const [present, setPresent] = useState(true);

  function sendMessage() {
    const value = message.trim();
    if (!value) return;

    setMessages((old) => [
      ...old,
      { role: "you", text: value },
      {
        role: "sidekick",
        text: "I hear you. I'm still a prototype, but this is where our conversation begins.",
      },
    ]);
    setMessage("");
  }

  return (
    <SafeAreaView style={styles.container}>
      <View style={styles.header}>
        <Text style={styles.brand}>SIDEKICK</Text>
        <Text style={styles.subtitle}>YOUR COMPANION</Text>
      </View>

      <View style={styles.identity}>
        <View style={styles.orb}>
          <Text style={styles.orbText}>S</Text>
        </View>
        <Text style={styles.name}>A presence of her own.</Text>
        <Text style={styles.status}>
          {present ? "● PRESENT" : "○ AWAY"}
        </Text>
        <TouchableOpacity
          style={styles.toggle}
          onPress={() => setPresent(!present)}
        >
          <Text style={styles.toggleText}>
            {present ? "Go away" : "Be present"}
          </Text>
        </TouchableOpacity>
      </View>

      <Text style={styles.section}>CONVERSATION</Text>

      <ScrollView style={styles.chat}>
        {messages.map((item, index) => (
          <View
            key={index}
            style={[
              styles.bubble,
              item.role === "you" ? styles.userBubble : styles.aiBubble,
            ]}
          >
            <Text style={styles.role}>
              {item.role === "you" ? "YOU" : "SIDEKICK"}
            </Text>
            <Text style={styles.message}>{item.text}</Text>
          </View>
        ))}
      </ScrollView>

      <View style={styles.inputArea}>
        <TextInput
          style={styles.input}
          value={message}
          onChangeText={setMessage}
          placeholder="Talk to me..."
          placeholderTextColor="#777"
          onSubmitEditing={sendMessage}
        />
        <TouchableOpacity style={styles.send} onPress={sendMessage}>
          <Text style={styles.sendText}>↑</Text>
        </TouchableOpacity>
      </View>

      <Text style={styles.footer}>
        YOUR SPACE. YOUR COMPANION. YOUR CHOICE.
      </Text>
    </SafeAreaView>
  );
}

const styles = StyleSheet.create({
  container: { flex: 1, backgroundColor: "#101713", padding: 22 },
  header: { alignItems: "center", marginTop: 20 },
  brand: { color: "#F2EBDD", fontSize: 27, letterSpacing: 7, fontWeight: "300" },
  subtitle: { color: "#9EAA9F", fontSize: 9, letterSpacing: 4, marginTop: 8 },
  identity: { alignItems: "center", marginVertical: 35 },
  orb: {
    width: 112, height: 112, borderRadius: 56,
    backgroundColor: "#294D3B", justifyContent: "center",
    alignItems: "center", borderWidth: 1, borderColor: "#78977C",
  },
  orbText: { color: "#F2EBDD", fontSize: 42, fontWeight: "200" },
  name: { color: "#F2EBDD", fontSize: 19, marginTop: 19 },
  status: { color: "#A7C5A8", fontSize: 10, letterSpacing: 3, marginTop: 12 },
  toggle: { padding: 10, marginTop: 8 },
  toggleText: { color: "#B8C8B8", fontSize: 12 },
  section: { color: "#8E9C91", fontSize: 10, letterSpacing: 3, marginBottom: 12 },
  chat: { flex: 1 },
  bubble: { padding: 16, borderRadius: 15, marginBottom: 12, maxWidth: "90%" },
  aiBubble: { backgroundColor: "#202D25", alignSelf: "flex-start" },
  userBubble: { backgroundColor: "#34533F", alignSelf: "flex-end" },
  role: { color: "#A9BCA9", fontSize: 9, letterSpacing: 2, marginBottom: 7 },
  message: { color: "#F2EBDD", fontSize: 15, lineHeight: 23 },
  inputArea: { flexDirection: "row", marginTop: 12, gap: 9 },
  input: {
    flex: 1, backgroundColor: "#202923", borderRadius: 14,
    padding: 15, color: "#F2EBDD", fontSize: 15,
  },
  send: {
    width: 52, borderRadius: 14, backgroundColor: "#78977C",
    justifyContent: "center", alignItems: "center",
  },
  sendText: { color: "#101713", fontSize: 25 },
  footer: { color: "#68776C", fontSize: 8, textAlign: "center", letterSpacing: 2, marginTop: 18 },
});


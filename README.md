
import React, { useState } from 'react';
import {
  View,
  Text,
  TextInput,
  ScrollView,
  Pressable,
  StyleSheet,
  SafeAreaView,
  StatusBar
} from 'react-native';
import * as Speech from 'expo-speech';

export default function App() {
  const [message, setMessage] = useState('');
  const [messages, setMessages] = useState([]);
  const [voice, setVoice] = useState(true);
  const [present, setPresent] = useState(true);

  const speak = (text) => {
    if (voice) Speech.speak(text, { rate: 0.92, pitch: 1.0 });
  };

  const sendMessage = () => {
    if (!message.trim()) return;
    const text = message.trim();
    setMessages(prev => [...prev, { text, from: 'you' }]);
    setMessage('');

    const reply = "I'm here. I'm listening. Let's figure it out together.";
    setTimeout(() => {
      setMessages(prev => [...prev, { text: reply, from: 'sidekick' }]);
      speak(reply);
    }, 500);
  };

  return (
    <SafeAreaView style={styles.safe}>
      <StatusBar barStyle="light-content" />
      <ScrollView contentContainerStyle={styles.container}>
        <View style={styles.header}>
          <Text style={styles.logo}>SIDEKICK</Text>
          <Text style={styles.version}>PERSONAL COMPANION · PROTOTYPE</Text>
        </View>

        <View style={styles.presence}>
          <View style={styles.orb}>
            <Text style={styles.orbText}>S</Text>
          </View>
          <Text style={styles.name}>I'm here.</Text>
          <Text style={styles.subtitle}>
            A presence that grows with you.
          </Text>
          <View style={styles.status}>
            <View style={styles.dot} />
            <Text style={styles.statusText}>
              {present ? 'PRESENT' : 'PAUSED'}
            </Text>
          </View>
        </View>

        <View style={styles.card}>
          <Text style={styles.section}>YOUR COMPANION</Text>
          <Text style={styles.cardTitle}>An identity of her own.</Text>
          <Text style={styles.description}>
            SIDEKICK is designed to develop her own identity,
            communicate naturally, and build continuity
            through conversations.
          </Text>
          <Text style={styles.tag}>IDENTITY · AUTONOMY · CONNECTION</Text>
        </View>

        <View style={styles.card}>
          <Text style={styles.section}>VOICE</Text>
          <Text style={styles.cardTitle}>Talk naturally.</Text>
          <Text style={styles.description}>
            Enable spoken responses and experience
            your companion's voice.
          </Text>
          <Pressable
            style={styles.button}
            onPress={() => {
              setVoice(!voice);
              if (!voice) Speech.speak("Voice is enabled.");
            }}>
            <Text style={styles.buttonText}>
              {voice ? 'VOICE ON  ✓' : 'ENABLE VOICE'}
            </Text>
          </Pressable>
          <Pressable
            style={styles.secondary}
            onPress={() => speak("Hello. I'm here with you.")}>
            <Text style={styles.secondaryText}>TEST VOICE</Text>
          </Pressable>
        </View>

        <View style={styles.card}>
          <Text style={styles.section}>CONVERSATION</Text>
          <Text style={styles.cardTitle}>Start somewhere.</Text>
          {messages.map((item, index) => (
            <View key={index} style={[
              styles.message,
              item.from === 'you' ? styles.userMessage : styles.aiMessage
            ]}>
              <Text style={styles.messageLabel}>
                {item.from === 'you' ? 'YOU' : 'SIDEKICK'}
              </Text>
              <Text style={styles.messageText}>{item.text}</Text>
            </View>
          ))}
          <TextInput
            style={styles.input}
            placeholder="Say what's on your mind..."
            placeholderTextColor="#777"
            value={message}
            onChangeText={setMessage}
            multiline
          />
          <Pressable style={styles.button} onPress={sendMessage}>
            <Text style={styles.buttonText}>SEND MESSAGE →</Text>
          </Pressable>
          <Text style={styles.note}>
            Prototype responses are currently local demonstrations,
            not a connected AI conversation.
          </Text>
        </View>

        <View style={styles.card}>
          <Text style={styles.section}>PERMISSION MODEL</Text>
          <Text style={styles.cardTitle}>Hybrid by design.</Text>
          <Text style={styles.description}>
            SIDEKICK can help independently with appropriate
            digital tasks. Real-world consequential actions
            require your authorization before completion.
          </Text>
          <Text style={styles.tag}>HUMAN AUTHORIZATION PROTECTED</Text>
        </View>

        <Pressable
          style={styles.pause}
          onPress={() => setPresent(!present)}>
          <Text style={styles.pauseText}>
            {present ? 'PAUSE PRESENCE' : 'RETURN TO PRESENCE'}
          </Text>
        </Pressable>

        <Text style={styles.footer}>SIDEKICK · BUILT TO GROW</Text>
      </ScrollView>
    </SafeAreaView>
  );
}

const styles = StyleSheet.create({
  safe: { flex: 1, backgroundColor: '#090D12' },
  container: { padding: 22, paddingBottom: 50 },
  header: { marginTop: 25, marginBottom: 35 },
  logo: { color: '#F0F3F5', fontSize: 27, fontWeight: '800', letterSpacing: 5 },
  version: { color: '#718493', fontSize: 9, letterSpacing: 2, marginTop: 8 },
  presence: { alignItems: 'center', paddingVertical: 32 },
  orb: {
    width: 112, height: 112, borderRadius: 56,
    backgroundColor: '#183C39', borderWidth: 2,
    borderColor: '#5CC9A2', alignItems: 'center',
    justifyContent: 'center', marginBottom: 22
  },
  orbText: { color: '#9BF0CE', fontSize: 42, fontWeight: '300' },
  name: { color: '#F2F5F6', fontSize: 31, fontWeight: '600' },
  subtitle: { color: '#8998A5', marginTop: 9, fontSize: 14 },
  status: {
    flexDirection: 'row', alignItems: 'center',
    marginTop: 20, gap: 8
  },
  dot: { width: 7, height: 7, borderRadius: 5, backgroundColor: '#5CC9A2' },
  statusText: { color: '#5CC9A2', fontSize: 10, letterSpacing: 2 },
  card: {
    backgroundColor: '#121A22', borderRadius: 19,
    padding: 21, marginTop: 17, borderWidth: 1,
    borderColor: '#26343F'
  },
  section: { color: '#5CC9A2', fontSize: 10, letterSpacing: 2, marginBottom: 13 },
  cardTitle: { color: '#F1F4F5', fontSize: 21, fontWeight: '600' },
  description: { color: '#A0ADB7', fontSize: 14, lineHeight: 23, marginTop: 12 },
  tag: { color: '#6D9D91', fontSize: 9, letterSpacing: 1.4, marginTop: 20 },
  button: {
    backgroundColor: '#5CC9A2', borderRadius: 12,
    padding: 16, alignItems: 'center', marginTop: 18
  },
  buttonText: { color: '#071711', fontSize: 12, fontWeight: '800', letterSpacing: 1.5 },
  secondary: {
    borderWidth: 1, borderColor: '#40534F',
    borderRadius: 12, padding: 15, alignItems: 'center', marginTop: 10
  },
  secondaryText: { color: '#B7DCCF', fontSize: 11, letterSpacing: 1.5 },
  input: {
    backgroundColor: '#202B35', borderRadius: 12,
    color: '#FFFFFF', padding: 15, minHeight: 55,
    marginTop: 15, fontSize: 14
  },
  message: { padding: 13, borderRadius: 12, marginTop: 12 },
  userMessage: { backgroundColor: '#263B3B' },
  aiMessage: { backgroundColor: '#202B35' },
  messageLabel: { color: '#5CC9A2', fontSize: 9, marginBottom: 6, letterSpacing: 1 },
  messageText: { color: '#F1F4F5', fontSize: 14, lineHeight: 21 },
  note: { color: '#71808D', fontSize: 10, lineHeight: 16, marginTop: 13 },
  pause: {
    borderWidth: 1, borderColor: '#52616B',
    padding: 17, borderRadius: 12, marginTop: 22,
    alignItems: 'center'
  },
  pauseText: { color: '#BBC6CC', fontSize: 11, letterSpacing: 2 },
  footer: { color: '#52616B', textAlign: 'center', marginTop: 30, fontSize: 10, letterSpacing: 3 }
});

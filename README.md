# Scripts

from burp import IBurpExtender, IIntruderPayloadProcessor

class BurpExtender(IBurpExtender, IIntruderPayloadProcessor):
    def registerExtenderCallbacks(self, callbacks):
        self._callbacks = callbacks
        self._helpers = callbacks.getHelpers()
        callbacks.setExtensionName("Continue After Success")
        callbacks.registerIntruderPayloadProcessor(self)
    
    def getProcessorName(self):
        return "Continue After Success"
    
    def processPayload(self, currentPayload, originalPayload, baseValue):
        # Modify this part to handle the response and continue the attack
        response = self._helpers.bytesToString(currentPayload)
        if "Success" in response:
            # Logic to continue the attack
            return originalPayload
        return currentPayload

<div class="comments-list">
  <div class="comment">
    <!-- Botón de Responder al lado derecho -->
    <button class="reply-button">Reply</button>

    <!-- Botones de Votación -->
    <div class="vote-buttons">
      <button>-</button>
      <span>0</span>
      <button>+</button>
    </div>

    <div>
      <div class="comment-header">
        <span><strong>Username</strong></span>
      </div>
      <p>Comment content</p>
      <button>Edit</button>
      <button>Delete</button>
    </div>
  </div>
</div>

<style>
  .comments-list {
    max-width: 600px;
    margin: 0 auto;
    font-family: Arial, sans-serif;
  }

  .comment {
    margin-bottom: 20px;
    padding: 10px;
    border: 1px solid #ddd;
    border-radius: 5px;
    display: flex;
    justify-content: flex-start;
    position: relative;
  }

  .comment-header {
    font-weight: bold;
  }

  textarea {
    width: 100%;
    margin-top: 10px;
    margin-bottom: 10px;
    padding: 8px;
    border: 1px solid #ddd;
    border-radius: 5px;
  }

  .vote-buttons {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    margin-right: 20px;
  }

  .vote-buttons button {
    margin-bottom: 5px;
    padding: 5px 10px;
    background: #007bff;
    color: white;
    border: none;
    border-radius: 5px;
    cursor: pointer;
  }

  .vote-buttons button:hover {
    background: #0056b3;
  }

  .vote-buttons span {
    font-size: 16px;
    font-weight: bold;
    margin-bottom: 10px;
  }

  button {
    margin-right: 5px;
    padding: 5px 10px;
    background: #e0e0e0;
    border: 1px solid #ccc;
    border-radius: 5px;
    cursor: pointer;
  }

  button:hover {
    background: #d0d0d0;
  }

  .deleted {
    color: #888;
    font-style: italic;
  }

  .reply-button {
    position: absolute;
    top: 10px;
    right: 10px;
    background-color: #28a745;
    color: white;
    border: none;
    border-radius: 5px;
    padding: 5px 10px;
    cursor: pointer;
  }

  .reply-button:hover {
    background-color: #218838;
  }
</style>

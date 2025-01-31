<script>
  import { writable } from 'svelte/store';
  
  // Store para almacenar los comentarios
  const comments = writable([
    { id: 1, user: 'amyrobson', content: 'This is amazing!', votes: 12, deleted: false, isEditing: false },
  ]);

  // Función para manejar votos positivos/negativos
  function vote(id, type) {
    comments.update(c => {
      const comment = c.find(c => c.id === id);
      if (comment) {
        if (type === "up") {
          comment.votes += 1;
        } else {
          comment.votes -= 1;
        }
      }
      return [...c];
    });
  }

  // Función para iniciar el modo de edición
  function startEdit(id) {
    comments.update(c => {
      const comment = c.find(c => c.id === id);
      if (comment) {
        comment.isEditing = true;
        comment.tempContent = comment.content; 
      }
      return [...c];
    });
  }

    // Función para guardar los cambios después de editar
    function saveEdit(id) {
    comments.update(c => {
      const comment = c.find(c => c.id === id);
      if (comment) {
        comment.content = comment.tempContent; 
        comment.isEditing = false; 
      }
      return [...c];
    });
  }

    // Función para cancelar la edición
    function cancelEdit(id) {
    comments.update(c => {
      const comment = c.find(c => c.id === id);
      if (comment) {
        comment.isEditing = false; 
      }
      return [...c];
    });
  }

    // Función para eliminar un comentario
    function deleteComment(id) {
    comments.update(c => {
      const comment = c.find(c => c.id === id);
      if (comment) {
        comment.deleted = true; 
      }
      return [...c];
    });
  }




</script>

<div class="comments-list">
  {#each $comments as comment (comment.id)}
  <div class="comment">
    <!-- Botón de Responder al lado derecho -->
    <button class="reply-button" on:click={() => replyToComment(comment.id)}>Reply</button>

        <!-- Botones de Votación -->
        <div class="vote-buttons">
          <button on:click={() => vote(comment.id, "down")}>-</button>
          <span>{comment.votes}</span>
          <button on:click={() => vote(comment.id, "up")}>+</button>
        </div>


        <div>
          <div class="comment-header">
            <span><strong>{comment.user}</strong></span>
          </div>

          {#if comment.isEditing}
            <textarea bind:value={comment.tempContent}></textarea>
            <button on:click={()=> saveEdit(comment.id)}>Save</button>
            <button on:click={() => cancelEdit(comment.id)}>Cancel</button>
          {:else}
            <p>{comment.content}</p>
            <button on:click={() => startEdit(comment.id)}>Edit</button>
            <button on:click={() => deleteComment(comment.id)}>Delete</button>
          {/if}
        </div>
   
  </div>
  {/each}
</div>

<style>
  :global(body){
    background: #e8e8e8;
  }
  .comments-list {
    max-width: 600px;
    margin: 0 auto;
    font-family: Arial, sans-serif;
  }

  .comment {
    border-width: 1px;
    border-color: rgba(219, 234, 254, 1);
    border-radius: 1rem;
    background-color: rgba(255, 255, 255, 1);
    padding: 1rem;
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
